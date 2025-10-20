# 🔗 鏈結串列（Linked List）進階變體與應用

## 🧩 一、鏈結串列的進階變體（Variants）

### 1️⃣ 雙向鏈結串列（Doubly Linked List）
結構：
```
NULL ← [prev|data|next] ⇄ [prev|data|next] ⇄ [prev|data|next] → NULL
```
每個節點有兩個指標：
- `prev`：指向前一個節點  
- `next`：指向下一個節點  

**優點：**
- 可以雙向遍歷  
- 可快速刪除指定節點（若已知指標）  
- 用於 LRU Cache、編輯器 Undo/Redo 系統  

**缺點：**
- 記憶體成本更高（多一個指標）  
- 插入 / 刪除操作要同時更新 `prev` 和 `next`  

---

### 2️⃣ 循環鏈結串列（Circular Linked List）
結構：
```
head → A → B → C ─┘
        ↑__________|
```
最後一個節點的 `next` 連回第一個節點（形成閉環）。

**應用：**
- 環狀排程（Round-Robin Scheduling）  
- Josephus 問題（約瑟夫環）  
- 音樂播放清單循環模式  

---

### 3️⃣ 跳躍表（Skip List）
結構概念：
```
Level 3:    A ───────────────> H
Level 2:    A ─────> D ─────> H
Level 1:    A → B → C → D → E → F → G → H
```
**優點：**
- 搜尋、插入、刪除平均時間：O(log n)  
- 比平衡樹更容易實作  

**應用：**
- Redis 的有序集合（ZSET）  
- LSM-Tree 結構中的 MemTable  

---

### 4️⃣ 自我調整鏈結串列（Self-Adjusting List）
每當某個元素被存取，就移動到開頭（Move-to-Front）。

**應用：**
- 模擬 LRU Cache  
- 頻繁重複查詢的資料加速  

---

### 5️⃣ 多重鏈結串列（Multi-Linked List）
每個節點有多個指標（如 `nextRow`, `nextCol`）。

**應用：**
- GUI 元件佈局  
- 二維資料表（稀疏矩陣）  
- 圖結構的鄰接表（Adjacency List）  

---

### 6️⃣ 靜態鏈結串列（Static Linked List）
用陣列模擬指標：
```cpp
struct Node {
    int data;
    int next;
};
Node list[100];
```

**應用：**
- 不支援指標的環境  
- 嵌入式系統  

---

## ⚙️ 二、鏈結串列的進階應用（Applications）

### 🧠 記憶體管理（Memory Management）
- 管理空閒與已配置區塊  
- 用於作業系統與執行階段記憶體分配  

### 💾 LRU Cache
- 雙向鏈結串列 + Hash Map  
- O(1) 搜尋、插入、刪除  

### 🔄 Undo / Redo 系統
- 使用雙向鏈結串列保存操作歷史  

### 📋 任務排程（Scheduler）
- 循環鏈結串列管理多進程輪流執行  

### 🧮 圖的鄰接表（Adjacency List）
- 每個頂點連結一條鏈結串列存相鄰節點  

### 🎮 遊戲引擎與模擬系統
- 管理動態物件（角色、子彈、粒子等）  

### 🧱 編譯器與直譯器
- Token 串列、AST 子節點、Symbol Table 等皆可用鏈結結構  

---

## 🧮 三、工程級優化與延伸設計

### 記憶體池（Memory Pool）
- 預先分配記憶體節點池，減少 new/delete 開銷  

### Lock-Free Linked List（無鎖鏈結串列）
- 使用 CAS 實現多執行緒安全操作  

### Persistent Linked List（持久化鏈結串列）
- 修改建立新版本，用於函數式語言或版本控制系統  

---

## ✅ 四、總結表

| 變體 | 特點 | 應用 |
|------|------|------|
| 雙向鏈結串列 | 雙向移動 | LRU Cache、Undo/Redo |
| 循環鏈結串列 | 無尾節點 | 排程系統、Josephus 問題 |
| 跳躍表 | 多層索引 | Redis Sorted Set |
| 多重鏈結串列 | 多維連結 | 圖、稀疏矩陣 |
| 自我調整串列 | 熱點加速 | Cache 模型 |
| 靜態鏈結串列 | 無指標 | 嵌入式系統 |
| Lock-Free | 無鎖高併發 | 網路伺服器 |
| Persistent | 多版本保存 | 函數式語言、Git |

---

> **總結：** 鏈結串列的威力，不在它的基本形態，而在它被改造後的多樣應用。
