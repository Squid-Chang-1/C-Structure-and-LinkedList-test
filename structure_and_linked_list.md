# 結構（Structure）與鏈結串列（Linked List）

---

## 📘 結構（Structure）宣告

使用關鍵字 `struct` 宣告結構：

```c
struct Student {
    char name[50];
    int age;
    float grade;
};
```

---

## 🧩 結構體運算與成員存取

### 存取成員的兩種方式
1. 使用「`.`」點運算子  
2. 使用「`->`」箭頭運算子（透過指標）

---

### 範例：存取結構成員

```c
#include <stdio.h>

// 定義結構
struct Student {
    char name[50];
    int age;
    float grade;
};

int main() {
    struct Student s1 = {"Rahul", 20, 18.5};
    struct Student s2 = {.age = 18, .name = "Vikas", .grade = 22};

    printf("%s	%d	%.2f\n", s1.name, s1.age, s1.grade);
    printf("%s	%d	%.2f\n", s2.name, s2.age, s2.grade);

    return 0;
}
```

---

## ✏️ 如何更新／設定結構體中字串資料

參考：[W3Schools C Structs](https://www.w3schools.com/c/c_structs.php)

```c
#include <stdio.h>
#include <string.h>

struct myStructure {
  int myNum;
  char myLetter;
  char myString[30];  // 字串資料
};

int main() {
  struct myStructure s1;

  // 正確設定字串（使用 strcpy）
  strcpy(s1.myString, "Some text");

  printf("My string: %s", s1.myString);
  return 0;
}
```

---

## 🧭 Structure Pointer（結構指標）

參考：[GeeksforGeeks - Structure Pointer in C](https://www.geeksforgeeks.org/c/structure-pointer-in-c/)

### 使用箭頭運算子 `->` 存取成員

```c
#include <stdio.h>

struct A {
    int var;
};

int main() {
    struct A a = {30};
    struct A *ptr = &a;

    printf("%d", ptr->var);
    return 0;
}
```

### 使用點運算子 `.` 存取成員（搭配解參考）

```c
#include <stdio.h>
#include <string.h>

struct Student {
    int roll_no;
    char name[30];
    char branch[40];
    int batch;
};

int main() {
    struct Student s1 = {27, "Geek", "CSE", 2019};
    struct Student* ptr = &s1;

    printf("%d\n", (*ptr).roll_no);
    printf("%s\n", (*ptr).name);
    printf("%s\n", (*ptr).branch);
    printf("%d", (*ptr).batch);

    return 0;
}
```

---

## 📋 結構體的複製

```c
#include <stdio.h>
#include <string.h>

struct myStructure {
  int myNum;
  char myLetter;
  char myString[30];
};

int main() {
  struct myStructure s1 = {13, 'B', "A888168"};
  struct myStructure s2;

  s2 = s1;  // 複製整個結構

  s2.myNum = 30;
  s2.myLetter = 'C';
  strcpy(s2.myString, "你的學號");

  printf("%d %c %s\n", s1.myNum, s1.myLetter, s1.myString);
  printf("%d %c %s\n", s2.myNum, s2.myLetter, s2.myString);

  struct myStructure* ptr = &s1;
  printf("%d %c %s\n", ptr->myNum, ptr->myLetter, ptr->myString);

  return 0;
}
```

---

## 🧠 結構體記憶體對齊與填充（Padding）

參考：[知乎專欄](https://zhuanlan.zhihu.com/p/614269719)

### 範例程式

```c
#include <stdio.h>

typedef struct structa_tag {
    char       c;
    short int  s;
} structa_t;

typedef struct structb_tag {
    short int s;
    char      c;
    int       i;
} structb_t;

typedef struct structc_tag {
    char      c;
    double    d;
    int       s;
} structc_t;

typedef struct structd_tag {
    double    d;
    int       s;
    char      c;
} structd_t;

int main() {
    printf("sizeof(structa_t) = %lu\n", sizeof(structa_t));
    printf("sizeof(structb_t) = %lu\n", sizeof(structb_t));
    printf("sizeof(structc_t) = %lu\n", sizeof(structc_t));
    printf("sizeof(structd_t) = %lu\n", sizeof(structd_t));
    return 0;
}
```

**執行結果：**
```
sizeof(structa_t) = 4
sizeof(structb_t) = 8
sizeof(structc_t) = 24
sizeof(structd_t) = 16
```

---

## ⚙️ 使用 `#pragma pack` 減少填充

### 範例 1：預設對齊（有 Padding）

```cpp
#include <iostream>
using namespace std;

struct PackedStruct {
    char a;
    int b;
    char c;
};

int main() {
    PackedStruct ps;
    cout << "Size of PackedStruct: " << sizeof(ps) << " bytes" << endl;
    return 0;
}
```

**輸出：**
```
Size of PackedStruct: 12 bytes
```

---

### 範例 2：使用 `#pragma pack(1)` 移除 Padding

```cpp
#include <iostream>
using namespace std;

#pragma pack(1)
struct PackedStruct {
    char a;
    int b;
    char c;
};
#pragma pack()

int main() {
    PackedStruct ps;
    cout << "Size of PackedStruct: " << sizeof(ps) << " bytes" << endl;
    return 0;
}
```

**輸出：**
```
Size of PackedStruct: 6 bytes
```

---

## 🔗 從結構體到鏈結串列（Linked List）

參考：  
- [GeeksforGeeks - Linked List](https://www.geeksforgeeks.org/dsa/linked-list-data-structure/)  
- [Singly Linked List Tutorial](https://www.geeksforgeeks.org/dsa/singly-linked-list-tutorial/)

### 建立鏈結串列步驟
1. 建立第一個節點（head）  
2. 為節點分配記憶體並設定資料  
3. 將節點依序連接起來  
4. 最後一個節點的 `next` 設為 `NULL`

---

### C++ 範例

```cpp
#include<iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int new_data) {
        this->data = new_data;
        this->next = nullptr;
    }
};

int main() {
    Node* head = new Node(10);
    head->next = new Node(20);
    head->next->next = new Node(30);
    head->next->next->next = new Node(40);

    while (head != nullptr) {
        cout << head->data << " ";
        head = head->next;
    }
}
```

---

### Python 範例

```python
class Node:
    def __init__(self, new_data):
        self.data = new_data
        self.next = None

head = Node(10)
head.next = Node(20)
head.next.next = Node(30)
head.next.next.next = Node(40)

temp = head
while temp is not None:
    print(temp.data, end=" ")
    temp = temp.next
```

---

## 🧮 Link List 的常見運算

| 操作 (Operation) | 中文說明 |
|------------------|----------|
| Traversal | 遍歷單鏈錶 |
| Insertion | 插入（開頭、結尾、特定位置） |
| Deletion | 刪除（開頭、結尾、特定位置） |
| Searching | 搜尋是否存在特定鍵值 |
| Updating | 修改節點內容 |
| Reversal | 反轉鏈結串列 |

---

📚 **總結**
- `struct` 是 C/C++ 中建立複合資料型態的基礎。
- 可使用「`.`」或「`->`」操作結構成員。
- `#pragma pack` 可控制記憶體對齊。
- 結構體是鏈結串列（Linked List）的基礎資料單位。

---
