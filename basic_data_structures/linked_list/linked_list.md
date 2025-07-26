## 연결 리스트 (Linked List)

**연결 리스트**는 데이터를 \*\*노드(Node)\*\*의 형태로 저장하며, 각 노드가 다음 노드를 가리키는 **포인터(Pointer)** 또는 \*\*참조(Reference)\*\*를 가지고 연결되는 선형 자료구조입니다. 배열처럼 메모리 상에 연속적으로 저장되지 않고, 필요에 따라 메모리의 아무 곳에나 노드를 할당하고 연결합니다.

### 특징

  * **비연속적인 메모리 할당:** 각 노드는 메모리의 서로 다른 위치에 있을 수 있습니다. 노드들은 포인터를 통해 논리적으로 연결됩니다.
  * **동적인 크기:** 배열과 달리 연결 리스트는 크기가 고정되어 있지 않습니다. 필요한 만큼 노드를 추가하거나 삭제할 수 있어 메모리를 효율적으로 사용할 수 있습니다.
  * **삽입 및 삭제의 효율성:** 특정 위치에 노드를 삽입하거나 삭제할 때, 해당 노드의 앞뒤 노드의 포인터만 변경하면 되므로 $O(1)$의 시간 복잡도를 가집니다 (단, 해당 노드를 찾아내는 데는 $O(N)$이 소요될 수 있음).
  * **접근의 비효율성:** 특정 인덱스의 요소에 접근하려면 리스트의 처음부터 순차적으로 탐색해야 하므로 $O(N)$의 시간 복잡도를 가집니다. 배열처럼 $O(1)$로 직접 접근할 수 없습니다.
  * **포인터 오버헤드:** 각 노드가 데이터를 저장하는 공간 외에 다음 노드의 주소를 저장하는 포인터 공간을 추가로 필요로 합니다.

### 장점

  * **동적인 크기 조절:** 데이터의 삽입과 삭제가 빈번한 경우에 유리합니다.
  * **효율적인 삽입 및 삭제:** 리스트의 중간에서도 $O(1)$ (노드를 찾은 후)의 시간으로 삽입/삭제가 가능합니다.

### 단점

  * **느린 접근 속도:** 특정 요소에 접근하기 위해선 처음부터 순차 탐색해야 하므로 $O(N)$의 시간이 걸립니다.
  * **추가적인 메모리 사용:** 각 노드마다 포인터를 저장할 공간이 필요합니다.
  * **캐시 비효율성:** 메모리 상에 연속적으로 배치되지 않아 캐시 지역성을 활용하기 어렵습니다.

### 연결 리스트의 종류

  * **단일 연결 리스트 (Singly Linked List):** 각 노드가 다음 노드를 가리키는 하나의 포인터만 가집니다. 가장 기본적인 형태입니다.
  * **이중 연결 리스트 (Doubly Linked List):** 각 노드가 다음 노드뿐만 아니라 이전 노드도 가리키는 두 개의 포인터를 가집니다. 양방향 탐색이 가능합니다.
  * **원형 연결 리스트 (Circular Linked List):** 마지막 노드가 첫 번째 노드를 가리켜 원형 구조를 이룹니다.

### C++에서의 연결 리스트

C++에서는 클래스와 포인터를 사용하여 연결 리스트를 직접 구현합니다. `std::list`는 이중 연결 리스트를 구현한 표준 라이브러리 컨테이너입니다.

```cpp
#include <iostream> // 입출력을 위해 필요
#include <list>     // std::list를 사용하기 위해 필요

// --- 단일 연결 리스트 구현 (예시) ---
// 노드 구조체 정의
struct Node {
    int data;     // 데이터를 저장할 변수
    Node* next;   // 다음 노드를 가리키는 포인터

    // 생성자
    Node(int val) : data(val), next(nullptr) {}
};

class SinglyLinkedList {
private:
    Node* head; // 리스트의 첫 번째 노드를 가리키는 포인터

public:
    SinglyLinkedList() : head(nullptr) {}

    // 소멸자: 메모리 해제
    ~SinglyLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next_node = current->next;
            delete current;
            current = next_node;
        }
        head = nullptr; // head를 nullptr로 설정하여 dangling pointer 방지
    }

    // 리스트 끝에 노드 추가
    void append(int data) {
        Node* new_node = new Node(data);
        if (head == nullptr) {
            head = new_node;
        } else {
            Node* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = new_node;
        }
    }

    // 특정 위치에 노드 삽입 (index 0부터 시작)
    void insert(int index, int data) {
        if (index < 0) {
            std::cout << "유효하지 않은 인덱스입니다." << std::endl;
            return;
        }

        Node* new_node = new Node(data);
        if (index == 0) {
            new_node->next = head;
            head = new_node;
            return;
        }

        Node* current = head;
        for (int i = 0; i < index - 1; ++i) {
            if (current == nullptr) {
                std::cout << "인덱스가 리스트 범위를 벗어났습니다." << std::endl;
                delete new_node; // 할당된 노드 메모리 해제
                return;
            }
            current = current->next;
        }

        if (current == nullptr) { // 인덱스가 리스트 길이와 같을 때 (맨 끝에 추가)
            std::cout << "인덱스가 리스트 범위를 벗어났습니다. 맨 끝에 추가됩니다." << std::endl;
            append(data); // append 함수를 재활용
            delete new_node; // 새로 생성한 new_node는 사용하지 않으므로 해제
            return;
        }

        new_node->next = current->next;
        current->next = new_node;
    }


    // 특정 인덱스 노드 삭제 (index 0부터 시작)
    void remove(int index) {
        if (head == nullptr) {
            std::cout << "리스트가 비어 있습니다." << std::endl;
            return;
        }
        if (index < 0) {
            std::cout << "유효하지 않은 인덱스입니다." << std::endl;
            return;
        }

        if (index == 0) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        Node* current = head;
        for (int i = 0; i < index - 1; ++i) {
            if (current == nullptr || current->next == nullptr) {
                std::cout << "인덱스가 리스트 범위를 벗어났습니다." << std::endl;
                return;
            }
            current = current->next;
        }

        if (current->next == nullptr) {
            std::cout << "인덱스가 리스트 범위를 벗어났습니다." << std::endl;
            return;
        }

        Node* temp = current->next;
        current->next = temp->next;
        delete temp;
    }

    // 리스트 출력
    void display() {
        Node* current = head;
        if (current == nullptr) {
            std::cout << "리스트가 비어 있습니다." << std::endl;
            return;
        }
        while (current != nullptr) {
            std::cout << current->data;
            if (current->next != nullptr) {
                std::cout << " -> ";
            }
            current = current->next;
        }
        std::cout << std::endl;
    }
};


int main() {
    std::cout << "--- 사용자 정의 단일 연결 리스트 ---" << std::endl;
    SinglyLinkedList mySinglyList;
    mySinglyList.append(10);
    mySinglyList.append(20);
    mySinglyList.append(30);
    mySinglyList.display(); // 출력: 10 -> 20 -> 30

    mySinglyList.insert(1, 15); // 인덱스 1에 15 삽입
    mySinglyList.display(); // 출력: 10 -> 15 -> 20 -> 30

    mySinglyList.remove(2); // 인덱스 2 (원래 20) 삭제
    mySinglyList.display(); // 출력: 10 -> 15 -> 30

    mySinglyList.insert(0, 5); // 맨 앞에 5 삽입
    mySinglyList.display(); // 출력: 5 -> 10 -> 15 -> 30

    mySinglyList.remove(0); // 맨 앞 요소 삭제
    mySinglyList.display(); // 출력: 10 -> 15 -> 30

    // --- std::list 사용 예시 (이중 연결 리스트) ---
    std::cout << "\n--- std::list (C++ 표준 라이브러리 이중 연결 리스트) ---" << std::endl;
    std::list<int> myList;

    // 요소 추가 (뒤에 삽입)
    myList.push_back(100);
    myList.push_back(200);
    myList.push_back(300);

    // 요소 출력
    std::cout << "초기 std::list: ";
    for (int val : myList) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    // 앞에 요소 추가
    myList.push_front(50);
    std::cout << "push_front(50) 후: ";
    for (int val : myList) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    // 중간에 요소 삽입 (이터레이터 사용)
    auto it = myList.begin();
    std::advance(it, 2); // 두 칸 이동 (50, 100 다음 위치)
    myList.insert(it, 150);
    std::cout << "insert(150) 후: ";
    for (int val : myList) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    // 특정 요소 삭제 (값으로 삭제)
    myList.remove(200);
    std::cout << "remove(200) 후: ";
    for (int val : myList) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    // 특정 위치 요소 삭제 (이터레이터 사용)
    it = myList.begin();
    std::advance(it, 1); // 두 번째 요소 (현재 100)
    myList.erase(it);
    std::cout << "erase(100) 후: ";
    for (int val : myList) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### Python에서의 연결 리스트

Python에서는 기본적으로 C++처럼 포인터를 직접 다루지 않고 객체 참조를 사용합니다. `list` 타입이 동적 배열과 같은 역할을 하지만, 연결 리스트의 개념을 이해하기 위해 클래스를 사용하여 직접 구현해볼 수 있습니다. 실제 Python 프로그래밍에서는 C++의 `std::list`처럼 동작하는 표준 라이브러리 컨테이너는 없으며, 대부분의 경우 내장 `list`가 충분히 유연하고 효율적입니다.

```python
# --- 단일 연결 리스트 구현 (예시) ---

# 노드 클래스 정의
class Node:
    def __init__(self, data):
        self.data = data # 데이터를 저장할 변수
        self.next = None # 다음 노드를 가리킬 참조 (초기에는 None)

# 연결 리스트 클래스 정의
class LinkedList:
    def __init__(self):
        self.head = None # 리스트의 첫 번째 노드를 가리킬 참조 (초기에는 None)

    # 리스트 끝에 노드 추가
    def append(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    # 특정 위치에 노드 삽입 (index 0부터 시작)
    def insert(self, index, data):
        if index < 0:
            print("유효하지 않은 인덱스입니다.")
            return

        new_node = Node(data)
        if index == 0:
            new_node.next = self.head
            self.head = new_node
            return

        current = self.head
        for _ in range(index - 1):
            if current is None:
                print("인덱스가 리스트 범위를 벗어났습니다.")
                return
            current = current.next

        if current is None: # 인덱스가 리스트 길이와 같을 때 (맨 끝에 추가)
            print("인덱스가 리스트 범위를 벗어났습니다. 맨 끝에 추가됩니다.")
            self.append(data) # append 함수를 재활용
            return

        new_node.next = current.next
        current.next = new_node

    # 특정 인덱스 노드 삭제 (index 0부터 시작)
    def remove(self, index):
        if self.head is None:
            print("리스트가 비어 있습니다.")
            return
        if index < 0:
            print("유효하지 않은 인덱스입니다.")
            return

        if index == 0:
            self.head = self.head.next
            return

        current = self.head
        for _ in range(index - 1):
            if current is None or current.next is None:
                print("인덱스가 리스트 범위를 벗어났습니다.")
                return
            current = current.next

        if current.next is None:
            print("인덱스가 리스트 범위를 벗어났습니다.")
            return

        current.next = current.next.next

    # 리스트 출력
    def display(self):
        elements = []
        current = self.head
        if current is None:
            print("리스트가 비어 있습니다.")
            return
        while current:
            elements.append(str(current.data))
            current = current.next
        print(" -> ".join(elements))

if __name__ == "__main__":
    print("--- 사용자 정의 단일 연결 리스트 ---")
    my_linked_list = LinkedList()
    my_linked_list.append(10)
    my_linked_list.append(20)
    my_linked_list.append(30)
    my_linked_list.display() # 출력: 10 -> 20 -> 30

    my_linked_list.insert(1, 15) # 인덱스 1에 15 삽입
    my_linked_list.display() # 출력: 10 -> 15 -> 20 -> 30

    my_linked_list.remove(2) # 인덱스 2 (원래 20) 삭제
    my_linked_list.display() # 출력: 10 -> 15 -> 30

    my_linked_list.insert(0, 5) # 맨 앞에 5 삽입
    my_linked_list.display() # 출력: 5 -> 10 -> 15 -> 30

    my_linked_list.remove(0) # 맨 앞 요소 삭제
    my_linked_list.display() # 출력: 10 -> 15 -> 30
```