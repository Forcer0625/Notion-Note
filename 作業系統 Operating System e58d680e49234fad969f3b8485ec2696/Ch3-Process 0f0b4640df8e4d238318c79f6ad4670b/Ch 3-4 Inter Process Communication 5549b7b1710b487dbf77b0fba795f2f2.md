# Ch 3-4 Inter Process Communication

---

- **Independent Process**
    - 不影響其他Process
    - 不被其他Process影響
    - 資料不共享

- **Cooperating Process**
    - 會影響其他Process
    - 會被其他Process影響
    - 資料共享

## Cooperating Process

- **資訊共享**
    
    Process之間分享某些資訊，令功能或服務更加useful
    

- **提升運算速度**
    
    加快計算速度，如GPU就很擅長平行計算，一個畫面可能包含許多矩陣運算
    

- **模組化**
    
    把功能交給不同Process去執行，如瀏覽器，Process分別去抓影片、文字等
    

## Inter Process Communication (IPC)

`Cooperating Process需要IPC[機制](../Ch2-Operating%20System%20Structure%20dfd17f0c5d434700b3979a1a672a9eef/Ch%202-3%20Operating%20System%20Design%20and%20Implementaion%20bb6bc28da3814ebf91edd5e37212e96c.md)來運作`

主要有兩種策略:

![Untitled](Ch%203-4%20Inter%20Process%20Communication%205549b7b1710b487dbf77b0fba795f2f2/Untitled.png)

Message Passing

![Untitled](Ch%203-4%20Inter%20Process%20Communication%205549b7b1710b487dbf77b0fba795f2f2/Untitled%201.png)

Shared Memory

- **Message Passing**
    
    ### **實作**
    
    - `**send_msg()**`
        
        複製message到系統的message queue
        
    - `**receive_msg()**`
        
        從系統的message queue複製到自己的記憶體區塊
        
    - **優點:**
        
        要交換的資訊很小時好用、容易實作、沒有資料讀寫衝突要避免
        
    - **缺點:**
        
        要從記憶體複製資料，速度很**慢**；[MircoKernel](../Ch2-Operating%20System%20Structure%20dfd17f0c5d434700b3979a1a672a9eef/Ch%202-4%20Operating%20System%20Structure%20329feec8405946b6adab75defaccc23c.md)的效能不佳就是在此
        
    
    ### 同步
    
    - **Blocking (視為同步)**
        
        Process會**循序**地執行
        
        ⇒ Ex: Process會等到I/O做完、回傳資料完才繼續
        
    - **Non-Blocking (視為非同步)**
        
        Process會**平行**地執行
        
        ⇒ Ex: Process會一直詢問I/O有資料了沒，有多少送多少，包含此次資料有多大
        

- **Shared Memory**
    
    ### **實作**
    
    - **Create**
        
        Process在自己的記憶體區塊建立一塊**共享區域**
        
    - **Attach**
        
        其他Process要共享則**attach**上去，因為程式在執行的時候認為自己的記憶體是連續的，當多個Process要共享時會出問題，實際上是OS"**讓Process以為自己用的是一塊連續記憶體**"
        
    - **優點:**
        
        速度非常**快**，不需搬運資料
        
    - **缺點:**
        
        有**讀寫衝突**的問題，需要注意對資料的**保護**和**同步**