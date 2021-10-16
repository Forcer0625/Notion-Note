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
> - **對於執行緒**
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
>     由於將執行的是**不同程式碼**，原本共用code section的所有Thread也將**一併被覆蓋掉**
>     

## Signal Handling

## Thread Cancellation

## Thread Local Storage