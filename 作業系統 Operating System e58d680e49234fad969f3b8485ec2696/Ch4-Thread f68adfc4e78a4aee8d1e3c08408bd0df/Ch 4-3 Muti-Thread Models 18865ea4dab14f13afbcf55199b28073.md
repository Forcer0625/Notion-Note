# Ch 4-3 Muti-Thread Models

---

## Supporting Thread

`有了Thread的機制，接下來要思考如何在OS實現Thread的概念`

- **`fork()`**是OS實現**Multi-Process**的function
    
    ⇒ OS也需要實現Multi-Thread的function
    

### Thread主要分為兩種型態

1. **User Thread**
    - 在**user層級**提供對Thread的相關操作
    - 來自**User函式庫 ⇒ Function Call**
2. **Kernel Thread**
    - 在**kernel層級**提供對Thread的相關操作
    - 來自**OS本身 ⇒ System Call**

![Untitled](Ch%204-3%20Muti-Thread%20Models%2018865ea4dab14f13afbcf55199b28073/Untitled.png)

## MultiThreading Models

`有了來自不同層級的Thread Supporting Type，衍生出不同的多執行緒模型`

![Untitled](Ch%204-3%20Muti-Thread%20Models%2018865ea4dab14f13afbcf55199b28073/Untitled%201.png)

Many-To-One

![Untitled](Ch%204-3%20Muti-Thread%20Models%2018865ea4dab14f13afbcf55199b28073/Untitled%202.png)

One-To-One

![Untitled](Ch%204-3%20Muti-Thread%20Models%2018865ea4dab14f13afbcf55199b28073/Untitled%203.png)

Many-To-Many

- **Many-To-One**
    
    ### 說明
    
    ![Untitled](Ch%204-3%20Muti-Thread%20Models%2018865ea4dab14f13afbcf55199b28073/Untitled%204.png)
    
    - 來自早期**不支援kernel thread**的OS，會把多執行緒**當成一個Process**去處理(PCB)，使用者應用程式只會在**自己的記憶體區塊維護和操作多執行緒**的相關資訊，如Stack、Thread descriptor
    - 實際執行時Threads只會在CPU內**切換執行(Run Concurrently)**
    
    ### 效率: `高`
    
    只在使用者層級完成操作，只需要**call function**就好，**不用呼叫system call**去麻煩OS
    
    ### 實作難度: `低`
    
    只需要把library寫好就好，反正OS只當會作一個Process
    
    ### 問題
    
    - **Blocking Problem**
        
        由於對於不支援kernel thread的系統來說，雖然使用者應用程式有很多Thread，但對於沒有kernel thread的系統而言，只認得一個Process，因此只要**某個Thread發生需要waiting的事件**(如system call)時，系統會把**包含多執行的整個Process Block住**，造成計算資源的**浪費**
        
    - **無法平行執行**
        
        縱然有多個Thread，因為OS只認得一個Process，所以OS分配CPU時，只會**跑在一個CPU核心**上，變成**多執行緒在單一核心中切換(Run Concurrently)**，無法發揮Thread真正的效用，是致命傷，基本上只有早期的OS不支援kernel thread
        
- **One-To-One**
    
    ### 說明
    
    ![Untitled](Ch%204-3%20Muti-Thread%20Models%2018865ea4dab14f13afbcf55199b28073/Untitled%205.png)
    
    - OS分配使用者的執行緒到**對應的kernel thread**，由**kernel儲存和維護(TCB)**
    - kernel thread會去競爭計算資源，實現真正意義上的**平行計算**
    - 執行緒建立是以**system call**的形式，而非Many-To-One是function call
    
    ### 效率: `低`
    
    每個Thread都需要**對應到一個kernel thread**，造成**維護和操作的成本**大幅提高
    
    ### 實作難度: `中`
    
    雖然多了很多kernel thread，但其實只要有**核心功能(kernel mode operation)**，又因為是**One-To-One**，只要**執行user thread呼叫的底層操作**即可，但相較於視為單執行緒的Many-To-One而言，多執行緒實作上肯定來得複雜些
    
    ### 問題
    
    - **效率**
        
        過多的user thread會產生對應的kernel thread，使用者建立和操作都會呼叫到system call
        
- **Many-To-Many**
    
    ### 說明
    
    - 使kernel thread的數量 **≤** user thread的數量
    - 解決前面兩種模型的問題
        - Many-To-One: 沒有真的達到平行計算
        - One-To-Many: 可能太多thread造成overhead
    - 實作上**彈性最高**
    
    ### 效率: `佳`
    
    既能實現平行計算，又不至於需要都對應到所有user thread，**平衡**前面兩種模型的優缺點，不過對於thread還是要system call，運行效率自然在**兩者之間**
    
    ### 實作難度: `高`
    
    **考量的因素變多了**，難度也直線上升，比如說很難決定一個kernel thread可以對應到幾個user thread來滿足使用者的需求、不同thread的task要怎麼分配給不定數量的kernel thread、什麼時候該建立或消滅一個kernel thread來平衡效能和overhead的考量
    
- **Two-Level**
    
    ### 說明
    
    - 現今硬體的計算速度大幅提升，kernel thread的overhead變得越來越不重要
    - 結合Many-To-Many和One-To-One