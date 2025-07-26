## 스택 (Stack)

**스택**은 **후입선출(LIFO: Last-In, First-Out)** 원칙을 따르는 선형 자료구조입니다. 가장 나중에 삽입된 데이터가 가장 먼저 삭제되는 구조로, 마치 접시를 쌓아 올린 더미나 책을 쌓아 올린 더미와 같습니다. 데이터를 넣는 작업을 **푸시(Push)**, 데이터를 꺼내는 작업을 \*\*팝(Pop)\*\*이라고 합니다.

### 특징

  * **후입선출 (LIFO):** 가장 나중에 삽입된 요소가 가장 먼저 삭제됩니다.
  * **단일 끝점 (Top):** 스택의 모든 연산(삽입, 삭제, 조회)은 한쪽 끝인 \*\*탑(Top)\*\*에서만 이루어집니다.
  * **제한된 접근:** 스택의 중간 요소에는 직접 접근할 수 없습니다. 오직 맨 위의 요소만 접근할 수 있습니다.

### 장점

  * **간단한 구조:** 구현이 비교적 간단합니다.
  * **함수 호출 관리:** 운영체제나 컴파일러에서 함수 호출 스택, 지역 변수 저장 등에 광범위하게 사용됩니다.
  * **undo/redo 기능:** 텍스트 편집기 등에서 이전 상태로 되돌리거나 다시 앞으로 가는 기능을 구현할 때 사용됩니다.
  * **수식 계산:** 괄호 매칭, 후위 표기법(Postfix Notation) 계산 등에 활용됩니다.
  * **재귀 알고리즘:** 재귀 호출을 비재귀적인 방식으로 변환할 때 스택을 사용할 수 있습니다.

### 단점

  * **중간 요소 접근 불가능:** 큐와 마찬가지로 특정 위치의 데이터를 조회하거나 수정하기 어렵습니다.

### 스택의 주요 연산

  * **`push(item)`:** 스택의 맨 위(top)에 요소를 추가합니다.
  * **`pop()`:** 스택의 맨 위(top)에서 요소를 제거하고 반환합니다. 스택이 비어있으면 오류를 반환할 수 있습니다.
  * **`top()` 또는 `peek()`:** 스택의 맨 위(top)에 있는 요소를 반환하지만, 스택에서 제거하지는 않습니다. 스택이 비어있으면 오류를 반환할 수 있습니다.
  * **`isEmpty()`:** 스택이 비어있는지 확인합니다.
  * **`size()`:** 스택에 있는 요소의 개수를 반환합니다.

### 구현 방법

스택은 주로 두 가지 방식으로 구현할 수 있습니다.

1.  **배열 (Array) 기반:**
      * `top` 인덱스를 사용하여 스택의 맨 위를 나타냅니다.
      * `push`는 `top` 인덱스를 증가시키며 요소를 추가하고, `pop`은 요소를 반환하고 `top` 인덱스를 감소시킵니다.
      * 배열의 고정된 크기 때문에 스택 오버플로우(Stack Overflow, 스택이 꽉 찼을 때)나 스택 언더플로우(Stack Underflow, 스택이 비었을 때)를 처리해야 합니다.
2.  **연결 리스트 (Linked List) 기반:**
      * `top` 노드 포인터를 사용하여 스택의 맨 위를 나타냅니다.
      * `push`는 새 노드를 `top`에 추가하고 `top` 포인터를 새 노드로 변경합니다.
      * `pop`은 `top` 노드를 제거하고 `top` 포인터를 그 다음 노드로 변경합니다.
      * 동적으로 크기가 조절되므로 스택 오버플로우 걱정이 적습니다 (메모리가 허용하는 한).

### C++에서의 스택

C++에서는 `std::stack`이라는 표준 라이브러리 컨테이너 어댑터를 제공합니다. `std::stack`은 기본적으로 `std::deque`를 사용하여 구현되며, `std::vector`나 `std::list`와 같은 다른 시퀀스 컨테이너를 기반으로도 사용할 수 있습니다.

```cpp
#include <iostream> // 입출력을 위해 필요
#include <stack>    // std::stack을 사용하기 위해 필요
#include <vector>   // 벡터 기반 스택 구현을 위해 (예시)
#include <list>     // 리스트 기반 스택 구현을 위해 (예시)

// --- 배열 기반 스택 (간단한 예시) ---
// 실제 사용 시에는 std::stack을 사용하는 것이 일반적입니다.
class ArrayStack {
private:
    int* arr;
    int capacity;
    int top_idx; // 스택의 가장 위에 있는 요소의 인덱스

public:
    ArrayStack(int size) : capacity(size), top_idx(-1) { // 초기에는 스택이 비어있으므로 -1
        arr = new int[capacity];
    }

    ~ArrayStack() {
        delete[] arr;
    }

    void push(int item) {
        if (top_idx == capacity - 1) { // 스택이 가득 찼는지 확인
            std::cout << "Stack overflow! Cannot push " << item << std::endl;
            return;
        }
        arr[++top_idx] = item; // top_idx를 증가시키고 요소 삽입
        std::cout << "Pushed: " << item << std::endl;
    }

    int pop() {
        if (isEmpty()) { // 스택이 비어있는지 확인
            std::cout << "Stack underflow! Cannot pop." << std::endl;
            return -1; // 또는 예외 발생
        }
        int item = arr[top_idx--]; // 요소를 반환하고 top_idx를 감소시킴
        std::cout << "Popped: " << item << std::endl;
        return item;
    }

    int top() {
        if (isEmpty()) {
            std::cout << "Stack is empty. No top element." << std::endl;
            return -1; // 또는 예외 발생
        }
        return arr[top_idx];
    }

    bool isEmpty() {
        return top_idx == -1;
    }

    int size() {
        return top_idx + 1;
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Stack is empty." << std::endl;
            return;
        }
        std::cout << "Stack elements (Top to Bottom): ";
        for (int i = top_idx; i >= 0; --i) {
            std::cout << arr[i] << " ";
        }
        std::cout << std::endl;
    }
};

// --- 연결 리스트 기반 스택 (단일 연결 리스트 재활용) ---
// Node 구조체와 SinglyLinkedList 클래스를 앞서 구현한 것을 사용한다고 가정합니다.
// 여기서는 간략하게 스택에 필요한 부분만 구현합니다.

// Node 구조체 정의 (앞서 연결 리스트에서 정의한 것과 동일)
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class LinkedListStack {
private:
    Node* top_ptr; // 스택의 맨 위 노드를 가리키는 포인터
    int current_size;

public:
    LinkedListStack() : top_ptr(nullptr), current_size(0) {}

    // 소멸자: 메모리 해제
    ~LinkedListStack() {
        while (!isEmpty()) {
            pop(); // 모든 노드 제거
        }
    }

    void push(int item) {
        Node* new_node = new Node(item);
        new_node->next = top_ptr; // 새 노드의 다음은 현재 top 노드
        top_ptr = new_node;       // top 포인터를 새 노드로 업데이트
        current_size++;
        std::cout << "Pushed: " << item << std::endl;
    }

    int pop() {
        if (isEmpty()) {
            std::cout << "Stack underflow! Cannot pop." << std::endl;
            return -1; // 또는 예외 발생
        }
        Node* temp = top_ptr; // 삭제할 노드 (현재 top)
        int item = temp->data;
        top_ptr = top_ptr->next; // top 포인터를 그 다음 노드로 업데이트
        delete temp;             // 이전 top 노드 메모리 해제
        current_size--;
        std::cout << "Popped: " << item << std::endl;
        return item;
    }

    int top() {
        if (isEmpty()) {
            std::cout << "Stack is empty. No top element." << std::endl;
            return -1; // 또는 예외 발생
        }
        return top_ptr->data;
    }

    bool isEmpty() {
        return top_ptr == nullptr; // 또는 current_size == 0;
    }

    int size() {
        return current_size;
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Stack is empty." << std::endl;
            return;
        }
        std::cout << "Stack elements (Top to Bottom): ";
        Node* current = top_ptr;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};


int main() {
    // --- std::stack 사용 예시 ---
    std::cout << "--- std::stack (C++ 표준 라이브러리) ---" << std::endl;
    std::stack<int> myStdStack;

    myStdStack.push(10); // Push
    myStdStack.push(20);
    myStdStack.push(30);

    std::cout << "Stack top: " << myStdStack.top() << std::endl; // Peek
    std::cout << "Stack size: " << myStdStack.size() << std::endl;

    myStdStack.pop(); // Pop
    std::cout << "After first pop, stack top: " << myStdStack.top() << std::endl;

    myStdStack.push(40);
    while (!myStdStack.empty()) {
        std::cout << "Popping: " << myStdStack.top() << std::endl;
        myStdStack.pop();
    }
    std::cout << "Is stack empty? " << (myStdStack.empty() ? "Yes" : "No") << std::endl;

    // --- 사용자 정의 배열 기반 스택 예시 ---
    std::cout << "\n--- 사용자 정의 배열 기반 스택 ---" << std::endl;
    ArrayStack arrStack(3); // 크기 3의 스택 생성

    arrStack.push(1);
    arrStack.push(2);
    arrStack.push(3);
    arrStack.push(4); // Stack overflow!
    arrStack.display(); // 3 2 1

    std::cout << "Top element: " << arrStack.top() << std::endl;

    arrStack.pop(); // 3
    arrStack.display(); // 2 1

    arrStack.pop(); // 2
    arrStack.pop(); // 1
    arrStack.pop(); // Stack underflow!
    arrStack.display(); // Stack is empty.

    // --- 사용자 정의 연결 리스트 기반 스택 예시 ---
    std::cout << "\n--- 사용자 정의 연결 리스트 기반 스택 ---" << std::endl;
    LinkedListStack llStack;

    llStack.push(100);
    llStack.push(200);
    llStack.push(300);
    llStack.display(); // 300 200 100

    std::cout << "Top element: " << llStack.top() << std::endl;

    llStack.pop(); // 300
    llStack.display(); // 200 100

    llStack.push(400);
    llStack.display(); // 400 200 100

    while (!llStack.isEmpty()) {
        llStack.pop();
    }
    llStack.display(); // Stack is empty.

    return 0;
}
```

### Python에서의 스택

Python에서는 내장 `list`가 스택의 모든 기능을 효율적으로 제공합니다. `append()`는 푸시 연산을, `pop()`은 팝 연산을 수행하며, 모두 `O(1)`의 시간 복잡도를 가집니다.

```python
# --- 리스트를 이용한 스택 (권장) ---
print("--- 리스트를 이용한 스택 ---")
my_stack = []

my_stack.append(10) # Push
my_stack.append(20)
my_stack.append(30)

print(f"현재 스택: {my_stack}") # [10, 20, 30]
print(f"스택의 가장 위 요소 (peek): {my_stack[-1]}") # 30

print(f"팝: {my_stack.pop()}") # Pop: 30
print(f"팝 후 스택: {my_stack}") # [10, 20]

my_stack.append(40) # Push
print(f"40 푸시 후 스택: {my_stack}") # [10, 20, 40]

print(f"스택의 크기: {len(my_stack)}")

while my_stack: # 스택이 비어있지 않은 동안
    print(f"팝: {my_stack.pop()}")
print(f"스택이 비었나요? {not my_stack}") # True

# collections.deque도 스택으로 사용할 수 있지만, list가 더 관용적입니다.
# from collections import deque
# my_stack_deque = deque()
# my_stack_deque.append(10) # push
# my_stack_deque.pop()     # pop
# print(my_stack_deque[-1]) # peek
```