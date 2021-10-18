# Ch 2-1 Operating System Service and Interface to Users

---

## Service

`作業系統提供許多功能，讓程式調用`

- **程式執行 Program Execution**
    - 保證程式可以被執行
    - Time-Sharing
- **輸出入 I/O operation**
    - 輸出
        
        ⇒ 螢幕、聲音、網路封包、VR螢幕、USB
        
    - 輸入
        
        ⇒ 鍵盤、滑鼠、麥克風、VR偵測、遊戲手把、USB
        
- **檔案系統 File System**
    - 管理/查看/覆寫檔案
        
        ⇒ 如windows檔案總管
        
    - 將檔案以某種方式呈現
        
        ⇒ 硬碟裡的資料可能是[碎裂](https://zh.wikipedia.org/wiki/%E7%A3%81%E7%9B%98%E7%A2%8E%E7%89%87)，需要檔案系統協助使用者存取
        
- **通訊 Communication**
    - Process間的溝通
        
        ⇒ 有些Process會影響其他Process，如多執行緒程式，共用的變數等
        
    - 系統間的溝通
        
        ⇒ 網際網路、區域網路
        
- **錯誤偵測 Error Detection**
    - 硬體錯誤
        
        ⇒ CPU、I/O、Memory、Hard disk等
        
    - 軟體錯誤
        
        ⇒ 除以0、沒有找到檔案等
        
- **保護與保全 Protection and Security**
    - Protection: 針對系統內部
        
        ⇒ 規範應用程式/使用者的存取權限，不能讓程式/非系統管理員凌駕於OS之上
        
    - Security: 針對系統外部
        
        ⇒ 保護系統免受網路攻擊、電腦病毒等
        
- **資源分配 Resource Allocation**
    - 分配程式執行的優先度/記憶體
    - 管理硬體資源，如記憶體，程式執行完，OS應釋放部分記憶體

## Interface

`使用者與作業系統互動`

- **命令列介面 Command-Line Interface**
    - 在GUI普及之前，使用者基本上透過CLI操作OS
    - 一種**程式**，並非作業系統的一部份
    - 可以直接輸入指令達成某些目的
- **批次介面 Batch Interface**
    - 將指令以**檔案**的方式**按順序**執行
    - 一項任務/功能可以被當成檔案**儲存**起來
- **圖形化使用者介面 Graphical User Interface**
    - 門檻低，操作上較直觀
    - 如Windows、Mac OS
- **觸控式螢幕介面 Touch Screen Interface**
    - 可以以**手勢**、**虛擬按鍵**操作
- **其他 Others**
    - 聲音，如語音助理Siri、Alexa
    - 動作，如虛擬實境