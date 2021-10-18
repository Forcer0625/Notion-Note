# Ch 3-1 Process Concept

---

## Overview

`"執行中"的程式，又稱job、task`

### **Program**

- 儲存在電腦硬碟中的**檔案**(二進制的可執行檔)
- 執行時被**載入到記憶體**讓CPU執行
- One-to-Many: **一個程式**可以產生**多個Process**

### Process

- 系統執行Process需要某些**資源**
- CPU: 利用**暫存器**運算、紀錄程式執行到哪裡和狀態
- 記憶體: Text、Data、Stack、Heap Sections
- 檔案

## Memory Scection in Process

![Untitled](Ch%203-1%20Process%20Concept%207e08818a4b2c48c19b2a6a7cc5910fd9/Untitled.png)

- **Stack Section**
    - 儲存**參數**、**回傳值位址**、**區域變數**
    - 所需空間**不固定**
    
    ![3-1 Stack.png](Ch%203-1%20Process%20Concept%207e08818a4b2c48c19b2a6a7cc5910fd9/3-1_Stack.png)
    
    CPU透過ESP暫存器來動態調整Stack大小
    
- **Heap Section**
    - 儲存**動態分配**的記憶體
    - 所需空間**不固定**
    - 以C為例: malloc()來宣告**使用**記憶體、free()來**釋放**記憶體 ⇒ 動態分配
- **Data Section**
    - 儲存**全域變數**，分為**已初始化**和**未初始化**的
    - 所需空間**固定**
    
    問題: 為什麼uninitialized data跟initialized data要分開(in C language)?
    
    ⇒ By definition, the bss segment takes some place in memory (when the program starts) but don't need any disk space
    
- **Text Section**
    - 儲存**程式碼/指令**，給Program Counter紀錄執行到哪，可以Branch到哪
    - 所需空間**固定**

## Process State

`Process在執行的時候，會改變其狀態(OS process management的結果)`

### States

- **new**
    
    程式被**載入到記憶體**
    
- **ready**
    
    可執行(Runnable)而未執行，若是執行中途的程式**狀態會被儲存**起來(PCB)
    
- **running**
    
    執行中，**占用CPU**
    
- **waiting**
    
    等待**特定事件**，通常為程式主動觸發如I/O或event wait()
    
- **terminated**
    
    Process**執行完畢**或**被OS終止**，會**釋放記憶體**
    
    為**不可逆操作**，因為其所需的記憶體空間**不再可靠** (可能系統拋棄相關的PCB或其他Process占用)
    

### **Process Control Block**

`OS對每個Process維護一個PCB，掌握某些資訊和狀態`

- Process State
- Program Counter
- CPU Registers
- CPU Secheduling Info
- Memory Management Info
- Accounting Info
- I/O status Info