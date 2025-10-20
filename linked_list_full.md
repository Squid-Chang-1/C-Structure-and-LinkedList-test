# 🚀 鏈結串列（Linked List）全解析

## 一、為什麼需要鏈結串列

在 C / C++ 中，陣列雖然方便，但有幾個限制：

| 問題 | 原因 |
|------|------|
| 大小固定 | 陣列宣告時大小必須固定，無法動態擴增。 |
| 插入刪除困難 | 插入或刪除中間元素要搬移整段記憶體。 |
| 記憶體碎片化 | 若用動態記憶體配置大陣列，可能失敗。 |

因此有了 **鏈結串列（Linked List）**：
> 用指標將分散的資料串接起來，讓資料結構更靈活。

---

## 二、鏈結串列的基本概念

每個節點（Node）包含：
- **資料區（data）**：儲存內容
- **連結區（next）**：指向下一個節點

### 節點示意圖
```
[Data | Next] -> [Data | Next] -> [Data | NULL]
```

---

## 三、C++ 基本實作

```cpp
class Node {
public:
    int data;
    Node* next;

    Node(int value) : data(value), next(nullptr) {}
};

int main() {
    Node* head = new Node(10);
    head->next = new Node(20);
    head->next->next = new Node(30);

    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}
```

輸出：
```
10 20 30
```

---

## 四、常見操作

### 插入節點（Insert）
```cpp
Node* newNode = new Node(5);
newNode->next = head;
head = newNode;
```

結果：
```
[5|*] -> [10|*] -> [20|*] -> [30|NULL]
```

### 刪除節點（Delete）
```cpp
Node* temp = head;
while (temp->next && temp->next->data != 20)
    temp = temp->next;
Node* toDelete = temp->next;
temp->next = temp->next->next;
delete toDelete;
```

結果：`10 -> 15 -> 30`

---

## 五、鏈結串列的種類

| 類型 | 結構 | 特點 |
|------|------|------|
| 單向鏈結串列 | head → A → B → C → NULL | 只能往一個方向走 |
| 雙向鏈結串列 | NULL ← A ⇄ B ⇄ C → NULL | 可往前或往後走 |
| 循環鏈結串列 | A → B → C → A | 形成閉環 |

---

## 六、時間複雜度

| 操作 | 陣列 | 鏈結串列 |
|------|------|-----------|
| 隨機存取 | O(1) | O(n) |
| 插入開頭 | O(n) | O(1) |
| 刪除開頭 | O(n) | O(1) |
| 搜尋元素 | O(n) | O(n) |

---

## 七、鏈結串列的缺點

### 1️⃣ 無法隨機存取
只能從頭逐一尋找。

### 2️⃣ 額外記憶體開銷
每個節點都需指標（64位元系統下為 8 Bytes）。

### 3️⃣ 快取效能差
節點分散記憶體中，Cache miss 機率高。

### 4️⃣ 指標操作易出錯
若指標未正確更新，可能導致 Crash。

### 5️⃣ 搜尋效率低
需逐一比對，O(n)。

### 6️⃣ 記憶體配置開銷高
每次 new/malloc 都需系統調用。

---

## 八、適用與不適用情境

| 情境 | 是否適合 |
|------|-----------|
| 資料固定 | ❌ |
| 頻繁插入刪除 | ✅ |
| 需要快取加速 | ❌ |
| 實作堆疊/佇列 | ✅ |

---

## 九、延伸應用

- Stack / Queue 實作  
- LRU Cache（雙向鏈結串列 + HashMap）  
- 記憶體區塊管理  
- 跳躍表（Skip List）

---

## 十、總結

| 優點 | 缺點 |
|------|------|
| 動態大小、靈活插入刪除 | 無法隨機存取 |
| 插入刪除效率高 | 記憶體開銷高 |
| 不需連續記憶體 | 快取效能差 |

---

✅ **一句話總結：**
> 鏈結串列適合「資料結構經常改變」但「查詢不頻繁」的情境。
