# Ch 2-3 Operating System Design and Implementaion

---

## Design Goal

`OS根據不同的需求有不同的設計方針`

### User Goal

- 針對**使用者體驗**
1. 方便使用
2. 容易上手
3. 可靠穩定
4. 安全隱私
5. 效能

### System Goal

- 針對**系統/程式設計師**
1. 容易設計/實作
2. 可維護性
3. 彈性高
4. Error-free
5. 效率

### 影響因素

- **硬體**
- **系統的類別**
    
    > 桌上型 Desktop
    移動型 Mobile
    分散式 Distributd
    即時 Real Time
    > 

## Mechanism and Policy

### 機制 Mechanism

`一件事的目標/方向/想要達成甚麼效果`

- 對策略的變化**不敏感**
    
    ⇒ 目標**不該**因為實作的方法而改變
    

### 策略 Policy

`一件事如何被實現的具體方法`

- 實作的方法或技術可能會**改變**或**被取代**
    
    ⇒ 如何**分離**機制和策略是系統設計的重要課題，Linux就是不錯的例子
    

### 舉例 Examples

- **微核心系統MicroKernel**
    
    機制: **保留最少的核心功能**，使系統所需空間不大
    
    策略: 以**核心模組**和**使用者程式**提供系統服務
    
- **Linux系統的工作排程**
    
    機制: Process**皆以優先權來執行**
    
    策略: 系統和使用者都可以對程序的優先權進行**調整**
    
- **~~2018高雄選舉~~**
    
    機制: ~~總目標是高雄發大財~~
    
    策略: ~~愛情摩天輪，簽署農產品銷售備忘錄，使貨出得去、人進得來~~
    

## Implementation

`作業系統發展至今，有許多方法可以設計一個作業系統`

- **組合語言 Assembly Language**
    - **MS-DOS**
        
        早期處理器速度不快，也沒有如今這麼多設計理念和經驗
        只能一行一行慢慢刻出來
        
    
    **優點:** 執行速度快
    **缺點:** 不容易維護、設計，移植性差
    
- **高階語言 High-level Language**
    - **Linux**
        
        90%的Linux程式碼由C編寫而來
        
    - **Android**
        
        使用的更多了，核心由C，系統函式庫由C++，應用程式框架以Java
        
    
    **優點:** 易維護，移植性高
    **缺點:** 執行速度取決於Complier，佔用空間大