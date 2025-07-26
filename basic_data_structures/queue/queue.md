## 큐 (Queue)

**큐**는 **선입선출(FIFO: First-In, First-Out)** 원칙을 따르는 선형 자료구조입니다. 먼저 들어온 데이터가 먼저 나가는 구조로, 마치 한 줄로 서서 기다리는 사람들의 줄과 같습니다. 데이터를 넣는 작업을 **인큐(Enqueue)**, 데이터를 꺼내는 작업을 \*\*디큐(Dequeue)\*\*라고 합니다.

### 특징

  * **선입선출 (FIFO):** 가장 먼저 삽입된 요소가 가장 먼저 삭제됩니다.
  * **두 개의 끝점:**
      * **프런트 (Front) 또는 헤드 (Head):** 큐에서 가장 먼저 나갈 요소가 있는 위치입니다. 디큐 연산이 일어나는 곳입니다.
      * **리어 (Rear) 또는 테일 (Tail):** 큐에 새로운 요소가 추가되는 위치입니다. 인큐 연산이 일어나는 곳입니다.
  * **제한된 접근:** 큐의 중간 요소에는 직접 접근할 수 없습니다. 오직 프런트와 리어에서만 연산이 가능합니다.

### 장점

  * **작업 스케줄링:** 운영체제에서 프로세스 스케줄링, 프린터 인쇄 대기열 등 처리 순서가 중요한 경우에 사용됩니다.
  * **버퍼링:** 데이터의 흐름을 임시로 저장하고 관리하는 데 유용합니다 (예: 네트워크 패킷 처리).

### 단점

  * **중간 요소 접근 불가능:** 특정 위치의 데이터를 조회하거나 수정하기 어렵습니다.
  * **고정 크기 배열 기반 큐의 한계:** 배열로 구현할 경우 `front`와 `rear` 포인터가 이동하면서 앞부분에 빈 공간이 생길 수 있으며, 이 공간은 재사용되지 않아 메모리 낭비가 발생할 수 있습니다 (이를 해결하기 위해 **원형 큐**가 사용됩니다).

### 큐의 주요 연산

  * **`enqueue(item)`:** 큐의 맨 뒤(rear)에 요소를 추가합니다.
  * **`dequeue()`:** 큐의 맨 앞(front)에서 요소를 제거하고 반환합니다. 큐가 비어있으면 오류를 반환할 수 있습니다.
  * **`front()` 또는 `peek()`:** 큐의 맨 앞(front)에 있는 요소를 반환하지만, 큐에서 제거하지는 않습니다. 큐가 비어있으면 오류를 반환할 수 있습니다.
  * **`isEmpty()`:** 큐가 비어있는지 확인합니다.
  * **`size()`:** 큐에 있는 요소의 개수를 반환합니다.

### 구현 방법

큐는 주로 두 가지 방식으로 구현할 수 있습니다.

1.  **배열 (Array) 기반:**
      * 고정된 크기를 가집니다.
      * `front`와 `rear` 인덱스를 사용하여 요소를 관리합니다.
      * \*\*원형 큐(Circular Queue)\*\*를 사용하여 배열의 앞쪽 공간 낭비를 해결할 수 있습니다.
2.  **연결 리스트 (Linked List) 기반:**
      * 동적으로 크기가 조절됩니다.
      * 노드의 추가 및 삭제가 `O(1)`으로 효율적입니다.
      * 별도의 `front`와 `rear` 노드 포인터를 유지하여 연산을 수행합니다.

### C++에서의 큐

C++에서는 `std::queue`라는 표준 라이브러리 컨테이너 어댑터를 제공합니다. `std::queue`는 기본적으로 `std::deque`를 사용하여 구현되며, 연결 리스트나 다른 컨테이너를 기반으로도 사용할 수 있습니다.

```cpp
#include <iostream> // 입출력을 위해 필요
#include <queue>    // std::queue를 사용하기 위해 필요
#include <vector>   // 벡터 기반 큐 구현을 위해 (예시)
#include <list>     // 리스트 기반 큐 구현을 위해 (예시)

// --- 배열 기반 큐 (간단한 예시, 원형 큐 아님) ---
// 실제 사용 시에는 원형 큐나 std::queue를 사용하는 것이 일반적입니다.
class ArrayQueue {
private:
    int* arr;
    int capacity;
    int front_idx;
    int rear_idx;
    int count; // 현재 큐에 있는 요소의 개수

public:
    ArrayQueue(int size) : capacity(size), front_idx(0), rear_idx(-1), count(0) {
        arr = new int[capacity];
    }

    ~ArrayQueue() {
        delete[] arr;
    }

    void enqueue(int item) {
        if (count == capacity) {
            std::cout << "Queue is full. Cannot enqueue " << item << std::endl;
            return;
        }
        rear_idx = (rear_idx + 1) % capacity; // 원형 큐처럼 인덱스 계산
        arr[rear_idx] = item;
        count++;
        std::cout << "Enqueued: " << item << std::endl;
    }

    int dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return -1; // 또는 예외 발생
        }
        int item = arr[front_idx];
        front_idx = (front_idx + 1) % capacity; // 원형 큐처럼 인덱스 계산
        count--;
        std::cout << "Dequeued: " << item << std::endl;
        return item;
    }

    int front() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element." << std::endl;
            return -1; // 또는 예외 발생
        }
        return arr[front_idx];
    }

    bool isEmpty() {
        return count == 0;
    }

    int size() {
        return count;
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        std::cout << "Queue elements: ";
        for (int i = 0; i < count; ++i) {
            std::cout << arr[(front_idx + i) % capacity] << " ";
        }
        std::cout << std::endl;
    }
};

// --- 연결 리스트 기반 큐 (단일 연결 리스트 재활용) ---
// Node 구조체와 SinglyLinkedList 클래스를 앞서 구현한 것을 사용한다고 가정합니다.
// 여기서는 간략하게 큐에 필요한 부분만 구현합니다.

// Node 구조체 정의 (앞서 연결 리스트에서 정의한 것과 동일)
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class LinkedListQueue {
private:
    Node* front_ptr;
    Node* rear_ptr;
    int current_size;

public:
    LinkedListQueue() : front_ptr(nullptr), rear_ptr(nullptr), current_size(0) {}

    // 소멸자: 메모리 해제
    ~LinkedListQueue() {
        while (!isEmpty()) {
            dequeue(); // 모든 노드 제거
        }
    }

    void enqueue(int item) {
        Node* new_node = new Node(item);
        if (isEmpty()) {
            front_ptr = new_node;
            rear_ptr = new_node;
        } else {
            rear_ptr->next = new_node;
            rear_ptr = new_node;
        }
        current_size++;
        std::cout << "Enqueued: " << item << std::endl;
    }

    int dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return -1; // 또는 예외 발생
        }
        Node* temp = front_ptr;
        int item = temp->data;
        front_ptr = front_ptr->next;
        if (front_ptr == nullptr) { // 마지막 요소 제거 시 rear_ptr도 nullptr로 설정
            rear_ptr = nullptr;
        }
        delete temp;
        current_size--;
        std::cout << "Dequeued: " << item << std::endl;
        return item;
    }

    int front() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element." << std::endl;
            return -1; // 또는 예외 발생
        }
        return front_ptr->data;
    }

    bool isEmpty() {
        return front_ptr == nullptr; // 또는 current_size == 0;
    }

    int size() {
        return current_size;
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        std::cout << "Queue elements: ";
        Node* current = front_ptr;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};


int main() {
    // --- std::queue 사용 예시 ---
    std::cout << "--- std::queue (C++ 표준 라이브러리) ---" << std::endl;
    std::queue<int> myStdQueue;

    myStdQueue.push(10); // Enqueue
    myStdQueue.push(20);
    myStdQueue.push(30);

    std::cout << "Queue front: " << myStdQueue.front() << std::endl; // Peek
    std::cout << "Queue size: " << myStdQueue.size() << std::endl;

    myStdQueue.pop(); // Dequeue
    std::cout << "After first pop, queue front: " << myStdQueue.front() << std::endl;

    myStdQueue.push(40);
    while (!myStdQueue.empty()) {
        std::cout << "Dequeuing: " << myStdQueue.front() << std::endl;
        myStdQueue.pop();
    }
    std::cout << "Is queue empty? " << (myStdQueue.empty() ? "Yes" : "No") << std::endl;

    // --- 사용자 정의 배열 기반 큐 예시 ---
    std::cout << "\n--- 사용자 정의 배열 기반 큐 ---" << std::endl;
    ArrayQueue arrQueue(5); // 크기 5의 큐 생성

    arrQueue.enqueue(1);
    arrQueue.enqueue(2);
    arrQueue.enqueue(3);
    arrQueue.display(); // 1 2 3

    arrQueue.dequeue(); // 1
    arrQueue.display(); // 2 3

    arrQueue.enqueue(4);
    arrQueue.enqueue(5);
    arrQueue.enqueue(6); // 큐가 꽉 찼습니다.
    arrQueue.display(); // 2 3 4 5

    std::cout << "Front element: " << arrQueue.front() << std::endl;
    std::cout << "Queue size: " << arrQueue.size() << std::endl;

    while (!arrQueue.isEmpty()) {
        arrQueue.dequeue();
    }
    arrQueue.display(); // Queue is empty.

    // --- 사용자 정의 연결 리스트 기반 큐 예시 ---
    std::cout << "\n--- 사용자 정의 연결 리스트 기반 큐 ---" << std::endl;
    LinkedListQueue llQueue;

    llQueue.enqueue(100);
    llQueue.enqueue(200);
    llQueue.enqueue(300);
    llQueue.display(); // 100 200 300

    std::cout << "Front element: " << llQueue.front() << std::endl;

    llQueue.dequeue(); // 100
    llQueue.display(); // 200 300

    llQueue.enqueue(400);
    llQueue.display(); // 200 300 400

    while (!llQueue.isEmpty()) {
        llQueue.dequeue();
    }
    llQueue.display(); // Queue is empty.

    return 0;
}
```

### Python에서의 큐

Python에서는 `list`를 사용하여 큐를 구현할 수 있지만, `list`의 `pop(0)` 연산은 `O(N)`의 시간 복잡도를 가져 비효율적입니다. 따라서 \*\*`collections` 모듈의 `deque` (double-ended queue)\*\*를 사용하는 것이 일반적이며, 이는 양방향 큐이므로 큐의 기능을 효율적으로 수행합니다 (`append()`와 `popleft()`가 `O(1)`).

```python
from collections import deque

# --- collections.deque를 이용한 큐 구현 (권장) ---
print("--- collections.deque를 이용한 큐 ---")
my_queue = deque()

my_queue.append(10)  # Enqueue
my_queue.append(20)
my_queue.append(30)

print(f"현재 큐: {my_queue}")
print(f"큐의 가장 앞 요소 (peek): {my_queue[0]}") # deque는 인덱스 접근 가능하지만, 큐의 원칙상 0만 접근

print(f"디큐: {my_queue.popleft()}")  # Dequeue
print(f"디큐 후 큐: {my_queue}")

my_queue.append(40)
print(f"40 인큐 후 큐: {my_queue}")

print(f"큐의 크기: {len(my_queue)}")

while my_queue: # 큐가 비어있지 않은 동안
    print(f"디큐: {my_queue.popleft()}")
print(f"큐가 비었나요? {not my_queue}") # True

# --- 리스트를 이용한 큐 (비효율적이지만 개념 이해를 위해) ---
print("\n--- 리스트를 이용한 큐 (비효율적) ---")
list_queue = []

list_queue.append(10) # Enqueue
list_queue.append(20)
list_queue.append(30)

print(f"현재 리스트 큐: {list_queue}")
print(f"큐의 가장 앞 요소 (peek): {list_queue[0]}")

print(f"디큐: {list_queue.pop(0)}") # Dequeue (O(N) 연산)
print(f"디큐 후 리스트 큐: {list_queue}")

list_queue.append(40)
print(f"40 인큐 후 리스트 큐: {list_queue}")

print(f"리스트 큐의 크기: {len(list_queue)}")

while list_queue:
    print(f"디큐: {list_queue.pop(0)}")
print(f"리스트 큐가 비었나요? {not list_queue}")
```