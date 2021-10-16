# Ch4-1 Overview

---

## Thread 執行緒

## Process 處理程序

- 多個執行緒屬於一個Process
- 滿足**平行計算**的需求，又不像Process有**太多Overhead**

![Untitled](Ch4-1%20Overview%205f611be15cac4f3ab46cf1ad8f6d2fed/Untitled.png)

- Content-Switch太慢
- Process占用太多資源
- 需要平行計算的前提下，有些Code或Data重複了

⇒ 執行緒**誕生的原因**

![Untitled](Ch4-1%20Overview%205f611be15cac4f3ab46cf1ad8f6d2fed/Untitled%201.png)

- **占用資源**
    - **Memory**
        
        Process記憶體內的**stack區域 ⇒ 小**
        
        建立一個執行緒**輕又快**
        
    - **狀態**
        - **Thread ID (tid)**
        - **Program Counter**
        - **Register Set**
            
            相當於狀態，執行緒雖同屬一個Process但是執行不同程度/任務的運算，包含**Stack Pointer**
            
        - **Thread Control Block**
            
            TCB儲存以上資訊
            
    - **Stack**
        
        執行緒可能有不同的行為，無法共用Stack，或者說，平行計算本身就不同狀態，一個Stack顯然不足以應付
        

- **占用資源**
    - **Memory**
        
        一塊**連續記憶體 ⇒ 大**
        
        建立一個Process**成本高又慢**
        
    - **狀態**
        - **Process ID (pid)**
        - **Program Counter**
        - **Register Set**
        - **Process Control Block**
            
            PCB儲存以上資訊
            
    - **Stack**

- **Muti-Threads共用資源**
    - **OS Resource**
        
        如開檔案、訊號傳遞/接收等
        
    - **Code Section**
        
        程式部分只要有效率地，分割運算量或分配任務，執行緒就會去排程占用CPU資源
        
    - **Data Section**
        - 同步/非同步問題
        - 比起Process間需要Message Passing或共用記憶體，大大減少資料溝通的成本

- **Muti-Process共用資源**
    
    很少，頂多部分記憶體(Shared-Region)