# Ch 4-6 Thread Issues

---

## Thread Pool

`由於建立和消滅執行緒很費時，不如把執行完的執行緒回收，既減少Thread的建立，也不用花時間回收Thread資源`

![Thread_pool.svg.png](Ch%204-6%20Thread%20Issues%20904114f9a62b459eadbf8858aee60450/Thread_pool.svg.png)

> **[Task Queue]**
> 
> 
> **針對Task做排程**，會把需要執行的**任務丟給執行緒池**中可用的執行緒
> 

> **[Thread Pool]**
> 
> 
> 存放多個執行緒，建立後**不會在短時間內消滅**，會持續執行Task Queue丟過來的Task
> 

**優點**

- **有效利用**系統花時間建立的執行緒
- 會**等待**可用的執行緒而不是頻繁建立執行緒**占用系統資源**
    
    ⇒ 保護多執行緒的Server免於類似DDos的攻擊
    

## Semantics of `fork()` and `exec()`

`有了Thread的概念後，回頭看原本用於Process的這兩個函式對於Thread背後的意義`

> `**fork()**`
> 
> - **原意**
>     
>     在Process中，`fork()`是把原本Process的memory section整個**複製**一份給不同pid的Process
>     
> - **對於執行緒 ⇒ Unix支援兩種版本**
>     1. 複製整個Process內的**所有執行緒**
>     2. 只複製**呼叫**`fork()`的執行緒

> `**exec()**`
> 
> - **原意**
>     
>     在Process中，`exec()`是把原本Process的memory section用其他程式**覆蓋**掉
>     
> - **對於執行緒**
>     
>     由於將執行的是**不同程式碼**，原本**共用**code section的所有Thread也將**一併被覆蓋掉**
>     

## Signal Handling

`當Process觸發**[Trap](../Ch1-Introduction%201a23cd5442fe44d8bd6e068d70edc8e6/Ch%201-4%20Operating%20System%20Operations%20f16d70d353834c279e44fc16bddca137.md)**的時候，OS會被執行，針對Event透過**訊號傳遞**的方式對Process做處理`

### 對於處理程序

- **OS 傳遞訊號** ⇒ Event-Driven
    1. 訊號由特定的事件**產生** 
    2. 訊號由觸發的Process**接收**
    3. 訊號由Process的**Signal Handler處理**
    
    ![Untitled](Ch%204-6%20Thread%20Issues%20904114f9a62b459eadbf8858aee60450/Untitled.png)
    
    UNIX訊號類型總表
    
- **Process 接收訊號** ⇒ Signal Handler
    1. [**User-Level**] Signal Handler
        - 來自**使用者**
        - 可以針對特定訊號**優先**對程式進行處理
            
            ⇒ 如Java的try&catch
            
    2. [**Kernel**] Signal Handler
        - 來自**作業系統**
        - 當使用者**沒有自定義**要如何處理訊號時使用**預設的方案**進行處理
            
            ⇒ 如程式存取到不該存取的記憶體時，終止該Process
            

### 對於執行緒

- **單執行程式** ⇒ 當作**一個Process**
- **多執行緒程式** ⇒ (預設)依照**訊號性質傳遞**
    1. **觸發訊號**的執行緒
        
        ⇒ 如呼叫[非法指令](../Ch1-Introduction%201a23cd5442fe44d8bd6e068d70edc8e6/Ch%201-4%20Operating%20System%20Operations%20f16d70d353834c279e44fc16bddca137.md)、除以0等
        
    2. **所有**的執行緒
        
        ⇒ 例如Ctrl+C終止處理程序，意味著**Process內的所有執行緒**也會被終止
        
    3. **特定**的執行緒
        
        ⇒ 用**tid指定**傳給哪個執行緒
        
    4. **專門處理訊號**的執行緒
        
        ⇒ 將訊號處理的操作**統一交由特定的執行緒**，方便大型程式維護
        

## Thread Cancellation

`在執行緒完成Task前終止，如資料庫搜尋用多執行緒加速，只要其中一個找到就讓其他執行緒終止`

### **非同步註銷 Asynchronous Cancellation**

- 將**Target Thread**立刻終止
- 對於執行緒占用的**資源在回收上**可能會有問題，例如編輯word，強行終止可能造成編輯遺失

### **延遲註銷(同步) Deferred Cancellation**

- 經由執行緒**週期性**的檢查是否被要求註銷(kill = 1)，較為**安全**
- 會在執行完**安全點**後終止，有點像玩遊戲要存檔，先**把資源卸下來**再繼續玩下一關

## Thread Local Storage

`執行緒需要有自己的資料，不與其他執行緒分享`

**Thread Local Storrage (TLS)**

- **Static**
    
    **⇒** 資料**生命週期**跟執行緒一樣長
    
- **不同於Stack**
    
    **⇒** 資料在函數執行完就沒了
    

![Untitled](Ch%204-6%20Thread%20Issues%20904114f9a62b459eadbf8858aee60450/Untitled%201.png)