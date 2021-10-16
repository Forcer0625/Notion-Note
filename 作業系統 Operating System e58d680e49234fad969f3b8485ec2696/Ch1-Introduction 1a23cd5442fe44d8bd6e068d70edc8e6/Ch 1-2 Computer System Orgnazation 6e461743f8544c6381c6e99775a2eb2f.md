# Ch 1-2 Computer System Orgnazation

---

## 電腦系統 Computer System

一個電腦系統包含
一個**中央處理器(CPU)**和
多個**裝置控制器(Device Controller)**
它們之間由**匯流排** **(Bus)**串聯起來

![Untitled](Ch%201-2%20Computer%20System%20Orgnazation%206e461743f8544c6381c6e99775a2eb2f/Untitled.png)

- **中央處理器 CPU**
    - 硬體
        
        `[General-Regsister]`
        
    - General-Purpose 通用
        
        可以做任何事，意味著可編程，不像傳統硬體只能用於特定用途，這也是為甚麼現在的電腦又叫做**通用計算機**
        
- **裝置控制器 Device Controller**
    - 硬體
        
        `[Special-Regsister]`
        
        `[Local Buffer]`
        
    - Special-Purpose
        
        一種裝置對應一種控制器
        
- **裝置驅動程式 Device Driver**
    - 軟體
        
        作業系統的一部份
        
    - 一種驅動程式對應一項裝置

### 硬體間的協作

1.  **CPU → Devices**
    
    裝置控制器是硬體，且是特殊用途，笨笨的，故操作皆**仰賴內部的暫存器**，因此CPU可藉由**讀寫**裝置控制器內的暫存器來告訴硬體要做什麼
    
2. **Devices → CPU**
    
    CPU是個大忙人，需要用**中斷(Interrupt)**來讓CPU知道某些資訊
    

## 中斷 Interrupt

*`表達硬體事件的訊號`*

- [1] **Raise** an Interrupt Signal
    
    裝置控制器會傳送訊號給PIC，PIC會根據優先度通知CPU
    
    ![Untitled](Ch%201-2%20Computer%20System%20Orgnazation%206e461743f8544c6381c6e99775a2eb2f/Untitled%201.png)
    
- [2] CPU **catch**
    
    CPU收到訊號並開始中斷處理，把PIC的interrupt訊號reset
    
- [3] CPU dispatch to **Interrupt Handler**
    
    中斷目前的Process，調用Interrupt Handler執行ISR(在記憶體上**固定的位置**)
    
    ![Untitled](Ch%201-2%20Computer%20System%20Orgnazation%206e461743f8544c6381c6e99775a2eb2f/Untitled%202.png)
    
- [4] CPU **serve**
    
    先把當前**狀態**存起來(暫存器)
    
    執行ISR
    
    復原**狀態**(回到Interrupt開始前的狀態，否則Process會出錯)
    
    ![Untitled](Ch%201-2%20Computer%20System%20Orgnazation%206e461743f8544c6381c6e99775a2eb2f/Untitled%203.png)
    

## **儲存裝置 Storage Structure**

- **Storage Device Hierachy**
    
    ![1_06strgDvcHrarch.jpg](Ch%201-2%20Computer%20System%20Orgnazation%206e461743f8544c6381c6e99775a2eb2f/1_06strgDvcHrarch.jpg)
