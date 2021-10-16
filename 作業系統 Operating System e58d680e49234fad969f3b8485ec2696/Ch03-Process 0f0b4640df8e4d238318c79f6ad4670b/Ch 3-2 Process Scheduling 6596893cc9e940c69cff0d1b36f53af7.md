# Ch 3-2 Process Scheduling

---

`OS維護多個針對不同狀態的佇列和排成演算法達到Process的多工`

## Scheduling Queue

`每個node儲存的是Process的狀態，也就是PCB`

- **Ready Queue**
    
    在記憶體，**隨時可以執行**的Process排隊的地方
    
- **Wait Queues**
    
    各種Process**需要等待**的事件，如I/O、Interrupt、Timer
    

## CPU Scheduling

`做排程的程式碼叫做CPU Scheduler`

### CPU Scheduler執行頻率

> **過高**
> 

可能CPU一直執行Scheduler，頻繁save/restore各個Process的狀態，造成Process實際上沒怎麼被執行

> **過低**
> 

Process回應時間時間過長
degree很小時，CPU可能會一直idle
degree太大時，Process會搶記憶體，可能在disk和記憶體之間一直swapping

### **Swapping (當Degree多到記憶體不夠用時)**

- **Swap out (-degree**
    
    系統會把等待中的Process放到硬碟去，以騰出空間給其他Process
    
- **Swap in   (+degree**
    
    CPU要執行時，將disk中的Process載入到記憶體
    

## Context Switch

`CPU從一個Process切換到另一個Process的過程`

- Process在PCB中的資訊就叫做Context (Environment)

### Step

1. Save current Process State
2. Run ISR (ISR固定，不需復原或儲存)
3. Restore State of next Process

### Overhead

排程本身就沒有在執行Process，算是某種意義上的CPU idle，因此花費的時間越少越好，**某些硬體**有以下方法可減少Context-Switch time

- **設計單一指令執行save/load**
    
    ⇒ 如x86架構的pushfd/popfd
    
- **Sun UltraSPARC系統提供多組的暫存器**
    
    ⇒ 就是以空間換時間，Context Switch就切換到某組暫存器