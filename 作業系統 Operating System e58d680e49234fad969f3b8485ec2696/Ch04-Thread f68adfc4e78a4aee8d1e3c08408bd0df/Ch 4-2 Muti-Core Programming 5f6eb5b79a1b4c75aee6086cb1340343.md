# Ch 4-2 Muti-Core Programming

---

## Concurrency & Parallelism

- **Concurrency**
    
    ![Untitled](Ch%204-2%20Muti-Core%20Programming%205f6eb5b79a1b4c75aee6086cb1340343/Untitled.png)
    
    同一個時間點只有一項Task在執行，只是**切換頻繁**到(人)錯以為同時在執行
    

- **Parallelism**
    
    ![Untitled](Ch%204-2%20Muti-Core%20Programming%205f6eb5b79a1b4c75aee6086cb1340343/Untitled%201.png)
    
    真正意義上的**同時執行**，當然也需要消耗計算資源(**Core**或**執行緒**)
    

## Types of Parallelism

**Data Parallelism**

![Untitled](Ch%204-2%20Muti-Core%20Programming%205f6eb5b79a1b4c75aee6086cb1340343/Untitled%202.png)

**Task Parallelism**

![Untitled](Ch%204-2%20Muti-Core%20Programming%205f6eb5b79a1b4c75aee6086cb1340343/Untitled%203.png)

- **分割資料**執行**相同任務**

- **共用資料**執行**不同任務**
- 實務上會將兩種策略混合運用，稱為**Hybird**，參見[**平行演算法**](https://zh.wikipedia.org/wiki/%E5%B9%B3%E8%A1%8C%E6%BC%94%E7%AE%97%E6%B3%95)

## Muti-Core Programming Challenge

`思考多執行緒程式會遇到的問題，通常也是軟體工程師的價值所在`

- **分割** **Divide Activites**
    
    在設計上要思考應用程式**如何切割成多執行緒來執行**或**加快運算速度**
    
- **平衡 Balance**
    
    硬體設計的關係，要思考如何平衡**每個執行緒的工作量**
    
- **資料拆分** **Data Splitting**
    
    **如何做**資料切割，**怎麼切**割分配到Core上
    
- **資料依賴 Data Dependency**
    
    軟體資料**相互關係**，具體來說一旦某個應用程式改變了，相應的資料也要隨之更新或改變
    
- **測試與偵錯Testing & Debugging**
    
    除了要驗證多執行緒效果外，偵錯也比單執行緒程式要難上許多