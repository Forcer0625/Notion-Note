# Ch 1-3 Computer System Architecture

---

## Single-Processor Systems

- 只有一個General-Purpose Processor和多個Special-Purpose Processor

## MultiProcessor  Systems

- 提升**產出量throughput**
    
    ⇒單位時間內可完成更多任務
    
- **Multi-Processors**
    - 多個Single-Core的Processor
        
        ![Untitled](Ch%201-3%20Computer%20System%20Architecture%20ce5e248dcf7f46768fa46ebe3d4acac3/Untitled.png)
        
    1. **Asymmetric Multiprocessing**
        
        只有一個Master Processor去控制多個Processor ⇒ **Master-slave**
        
    2. **Symmetric Multiprocessing `SMP`**
        
        Processor間對等，無主從之分
        
- **Multi-Core System**
    - 多個Core在一個chip上，共享部分cache ⇒ 溝通上快速，比SMP效率高
        
        ![Untitled](Ch%201-3%20Computer%20System%20Architecture%20ce5e248dcf7f46768fa46ebe3d4acac3/Untitled%201.png)
        
- **Non-Uniform Memory Access** `NUMA`
    - 多個CPU存取同一塊記憶體會造成**System Bus**上的瓶頸 ⇒ Processor不一定越多越好
    - 規劃CPU可存取的記憶體位置，各自透過**Local Bus**維護/管理自己的**記憶體區塊**
        
        ![Untitled](Ch%201-3%20Computer%20System%20Architecture%20ce5e248dcf7f46768fa46ebe3d4acac3/Untitled%202.png)
        
        ⇒ CPU存取到不是自己的記憶體區塊比存取自己的慢
        
- **Blade Server**
    - 多個處理機板`Processor Board`整合到一個Box內，每個機板可以獨立運行自己的OS
    - 統一提供電源、散熱、網路通訊等，便於集中管理
    
    [8U_SuperBlade.webp](Ch%201-3%20Computer%20System%20Architecture%20ce5e248dcf7f46768fa46ebe3d4acac3/8U_SuperBlade.webp)
    

## Clustered Systems

- 多個computer透過區域網路`[LAN](https://www.notion.so/CH01-Overview-32a102e826434019ac8aa5377489591d)`連起來
    
    ![Untitled](Ch%201-3%20Computer%20System%20Architecture%20ce5e248dcf7f46768fa46ebe3d4acac3/Untitled%203.png)
    
- **High Availability**
    
    不容易停止運行，在需要時多半能獲得服務/回應
    
    - **Graceful Degradation**
        
        效能隨著computer減少而可預期地遞減，與CPU數量成正比
        
        ![Untitled](Ch%201-3%20Computer%20System%20Architecture%20ce5e248dcf7f46768fa46ebe3d4acac3/Untitled%204.png)
        
    - **Fault Tolerant**
        
        一個computer無法工作不會影響整個系統運行