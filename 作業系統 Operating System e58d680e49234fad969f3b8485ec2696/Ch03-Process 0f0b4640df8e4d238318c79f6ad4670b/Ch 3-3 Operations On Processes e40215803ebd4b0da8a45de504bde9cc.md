# Ch 3-3 Operations On Processes

---

## Creation

### Process Tree

`一個Process可以(請OS)建立新的Process，彼此間形成parent-children的關係`

- 同一支程式可以產生的很多Process(如好幾個word)，每個Process有不同狀態，因此需要**Process Identifier(pid)**而非用程式名稱來區分

![Untitled](Ch%203-3%20Operations%20On%20Processes%20e40215803ebd4b0da8a45de504bde9cc/Untitled.png)

OS透過pid來識別不同的process

### Execution

- Parent跟Children一同執行: 如windows檔案總管跟Word
- Parent等Children執行完畢: 如程式使用`wait()`

### Address Space

- Children複製Parent的(相同狀態): 如`fork()` in Linux
    
    ⇒ `fork()` 成功會對Parent回傳Children的**pid**，失敗則傳**負值**
        對Children會回傳**0**
    

![Untitled](Ch%203-3%20Operations%20On%20Processes%20e40215803ebd4b0da8a45de504bde9cc/Untitled%201.png)

- Children載入新的程式: `exec()` in Linux
    
    ⇒ Process先fork，children再執行exec
    
    ![Untitled](Ch%203-3%20Operations%20On%20Processes%20e40215803ebd4b0da8a45de504bde9cc/Untitled%202.png)
    
    Example Code
    

![Untitled](Ch%203-3%20Operations%20On%20Processes%20e40215803ebd4b0da8a45de504bde9cc/Untitled%203.png)

![Untitled](Ch%203-3%20Operations%20On%20Processes%20e40215803ebd4b0da8a45de504bde9cc/Untitled%204.png)

## Termination

### 程式呼叫`exit()`來終止Process

- OS回傳Process的**status value**和**pid**給parent
    - 一般回傳0當作程式正常結束，值存於Process的PCB中
- Parent要用`wait()`來接收children的資訊
    
    ```c
    #include<sys/wait.h>
    pid_t wait(int *stat_loc)
    ```
    

### Zombie/Orphan Process

- **Zombie Process**
    
    Children在Parent呼叫`wait()`前就執行完畢了，但依然占用記憶體空間
    
- **Orphan Process**
    
    若Parent沒有呼叫`wait()`就先結束了，OS會主動接收Children的status value，避免成為Orphan Process占用記憶體，如Linux會透過**init**這個Process來接收