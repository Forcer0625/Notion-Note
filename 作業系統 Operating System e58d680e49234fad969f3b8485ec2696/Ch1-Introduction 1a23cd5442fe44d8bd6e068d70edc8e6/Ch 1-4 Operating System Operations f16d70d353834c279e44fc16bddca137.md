# Ch 1-4 Operating System Operations

---

## Event-Driven OS

`當以下事件發生時，CPU會執行作業系統相關的Service/Fuction，同時切換到Monitor Mode`

- **中斷** `[Interrupt](Ch%201-2%20Computer%20System%20Orgnazation%206e461743f8544c6381c6e99775a2eb2f.md)`
    - **硬體**觸發
- **Trap/Exception**
    - **軟體**觸發
    - **Error**
        - 除以0 Division by 0
            
            一般情況下OS會把發生除以0的程式shut down
            
        - 非法指令 [illegal Instruction]()
    - **[System Call/Monitor Call](../Ch2-Operating%20System%20Structure%20dfd17f0c5d434700b3979a1a672a9eef/Ch%202-2%20System%20Calls%20d3b86369505543cab81f8eae6701fb03.md)**
        
        ![Untitled](Ch%201-4%20Operating%20System%20Operations%20f16d70d353834c279e44fc16bddca137/Untitled.png)
        
        - 作業系統提供的函式
            
            ⇒ read(), open(), write()
            

## Multiprogramming and Multitasking

`你可以"同時"看影片、玩遊戲、聽音樂、下載文件、瀏覽網頁的原因`

- **Single-Programming System**
    - 一次只執行一項工作，執行完才會跑下一項
    - 超爛，比如說在等待I/O時，CPU就會待機(idle)
- **Multi-Programming System**
    - 盡可能使CPU一直在工作
        
        比如說程式A在等待I/O時，OS就可以分配其他程式讓CPU去跑
        
- **Time-Sharing/Multitasking System**
    - Multi-Programming的**問題**
        
        若程式沒有需要等待的時間，CPU可能會被一支程式占用很長時間，導致其他程式無法執行或回應很慢
        
    - **高互動性**
        
        比如說玩遊戲或編輯文件，需要鍵盤/滑鼠對使用者即時回饋
        
    - **週期性**地切換程式執行
        
        每支程式的回應時間大幅縮短
        
    - **計時器 Timer**
        
        `實現Time-Sharing System的硬體`
        
        - 週期性觸發Interrupt
            
            ⇒ 令CPU回到OS，OS才得以分配工作，從而實現Time-Sharing
            
        - 為什麼不用其他硬體?
            
            ⇒ 硬體除了CPU外都是**Special-Purpose**的，被設計用來專門做某些事
            

## Dual-Mode/Multi-Mode Operation

`有些程式會執行可能讓整個電腦系統崩潰的指令，需要加以區分`

- **Dual-Mode**
    
    CPU內部暫存器用**`Mode bit`**來區分
    
    - **0:** **User mode**
    - **1: Monitor/Kernel/Supervisor mode**
        
        ⇒ 有權限執行**privileged instruction**
        
- **Multi-Mode**
    - 有些處理器提供多層保護
        
        Ex: x86架構CPU支援4種模式(Ring 0~3)，OS執行在Ring 0 ←→ 應用程式在Rnig 3
        
- **特權指令 Privileged Instruction**
    - 某些指令可能會**危害**到整個系統的運行
        
        ⇒ 例如I/O control、Interrupt Management、Timer Management
        
    - 只能在**Monitor Mode**下被執行
        
        ⇒ 若在User Mode下執行，會當作一個**Trap**使CPU去執行OS