# Ch 2-2 System Calls

---

## Overview

作業系統提供許多功能供**程式**去調用

- 程式**呼叫System cal**l時，CPU會切換到OS執行
- OS會維護一個**表**，表上的**數字**一一對應到一種Call
- 不同OS有**不同**的System Call，如Win32、Java(虛擬機)
- 直接使用System call會降低程式的**可移植性**，一般都用高階語言的**API**

![Untitled](Ch%202-2%20System%20Calls%20d3b86369505543cab81f8eae6701fb03/Untitled.png)

### 參數傳入

`OS和程式之間透過彼此都能access的"公共空間"來傳遞資訊`

主要透過以下這些，**Cache歸硬體**管，軟體碰不到

- **暫存器 Register**
    - 速度**最快**
    - 空間**不大**
    - **數量**有限，參數不能超出可用的暫存器個數
- **記憶體 Memory**
    - 速度**次之**
    - 空間**夠大**，不太可能用完
    - 兩種模式
        1. **Block:** 程式劃定一區塊，位址放暫存器，裡面放各種參數，CPU處理時只需拿某一塊
        2. **Stack:** 程式push參數進stack，執行時OS再pop
- **硬碟 Hard Disk**
    - 速度**最慢**，一般不用這個方法
    - 可在程式**執行完後儲存**，意味著**斷電源**也行，例如程式的設定文件、遊戲存檔等

## System Programs

`作業系統提供舒適的環境和服務，使程式便於執行和開發`

![Untitled](Ch%202-2%20System%20Calls%20d3b86369505543cab81f8eae6701fb03/Untitled%201.png)