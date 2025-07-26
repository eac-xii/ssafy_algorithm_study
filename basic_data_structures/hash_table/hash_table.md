## 해시 테이블 (Hash Table)

**해시 테이블(Hash Table)**, 또는 \*\*해시 맵(Hash Map)\*\*은 \*\*키(Key)\*\*와 \*\*값(Value)\*\*을 연결하여 데이터를 저장하는 자료구조입니다. 특정 키를 입력하면 그에 해당하는 값을 매우 빠르게 찾을 수 있도록 설계되었습니다. 데이터의 삽입, 삭제, 검색이 평균적으로 $O(1)$의 시간 복잡도를 가집니다.

### 핵심 원리: 해싱 (Hashing)

해시 테이블의 핵심은 \*\*해싱(Hashing)\*\*입니다. 해싱은 임의의 크기를 가진 데이터를 고정된 크기의 값(해시 코드 또는 해시 값)으로 매핑하는 과정입니다. 이 해시 값을 배열의 \*\*인덱스(Index)\*\*로 사용하여 데이터를 저장하거나 검색합니다.

1.  **키(Key):** 저장하려는 데이터를 식별하는 고유한 값입니다.
2.  **해시 함수(Hash Function):** 키를 입력받아 배열의 유효한 인덱스(해시 값)로 변환하는 함수입니다. 좋은 해시 함수는 키들을 고르게 분포시켜 충돌(Collision)을 최소화해야 합니다.
3.  **해시 값(Hash Value) / 해시 코드(Hash Code):** 해시 함수가 키를 변환하여 생성하는 정수 값입니다. 이 값이 배열의 인덱스로 사용됩니다.
4.  **버킷(Bucket) / 슬롯(Slot):** 해시 테이블의 각 인덱스에 해당하는 공간으로, 실제 데이터(키-값 쌍)가 저장되는 곳입니다. 일반적으로 배열의 요소입니다.

### 특징

  * **빠른 탐색, 삽입, 삭제:** 평균적으로 $O(1)$의 시간 복잡도를 가집니다. 해시 함수를 통해 직접 저장 위치를 계산하기 때문입니다.
  * **키-값 쌍 저장:** 데이터를 키와 값의 형태로 저장합니다.
  * **충돌 처리:** 서로 다른 키가 동일한 해시 값을 생성하여 같은 버킷을 가리키는 \*\*충돌(Collision)\*\*이 발생할 수 있습니다. 이를 처리하는 방법이 중요합니다.

### 충돌 해결 방법 (Collision Resolution)

충돌은 해시 테이블의 성능에 큰 영향을 미치므로, 이를 효과적으로 해결하는 것이 중요합니다.

1.  **개별 체이닝 (Separate Chaining):**

      * 동일한 해시 값을 가진 모든 키-값 쌍을 **연결 리스트(Linked List)** 형태로 해당 버킷에 저장합니다.
      * 장점: 구현이 비교적 간단하고, 테이블이 거의 꽉 차더라도 성능 저하가 비교적 적습니다.
      * 단점: 연결 리스트를 위한 추가적인 메모리가 필요하고, 캐시 지역성이 좋지 않을 수 있습니다.

2.  **개방 주소법 (Open Addressing):**

      * 충돌이 발생하면 해시 테이블 내의 다른 빈 버킷을 찾아 데이터를 저장합니다.
      * **선형 탐사 (Linear Probing):** 충돌 발생 시, 다음 빈 버킷을 순차적으로 탐색합니다 (`index + 1`, `index + 2`, ...).
      * **제곱 탐사 (Quadratic Probing):** 충돌 발생 시, 제곱수를 더하여 빈 버킷을 탐색합니다 (`index + 1^2`, `index + 2^2`, ...).
      * **이중 해싱 (Double Hashing):** 두 번째 해시 함수를 사용하여 탐사 간격을 결정합니다.
      * 장점: 추가적인 메모리 구조가 필요 없으며, 캐시 효율성이 좋습니다.
      * 단점: **군집화(Clustering)** 문제가 발생할 수 있으며, 삭제가 복잡하고 테이블의 로드 팩터(Load Factor)가 높아지면 성능이 급격히 저하될 수 있습니다.

### 장점

  * 매우 빠른 데이터 접근, 삽입, 삭제 (평균 $O(1)$)
  * 키를 사용하여 데이터를 직관적으로 관리 가능

### 단점

  * 충돌 처리 방식에 따라 성능이 크게 좌우됨
  * 정렬된 데이터를 유지하기 어려움 (순서가 없음)
  * 키가 해시 함수에 의해 고르게 분포되지 않을 경우 성능 저하
  * 메모리 사용량이 예상보다 클 수 있음 (버킷 배열)

### 사용 예시

  * 데이터베이스 인덱싱
  * 캐시(Cache) 구현
  * 딕셔너리(Dictionary) 또는 맵(Map) 자료형의 내부 구현
  * 심볼 테이블 (컴파일러)
  * 네트워크 라우팅 테이블

### C++에서의 해시 테이블

C++에서는 `std::unordered_map`이 해시 테이블을 구현한 표준 라이브러리 컨테이너입니다.

```cpp
#include <iostream> // 입출력을 위해 필요
#include <string>   // 키로 문자열 사용
#include <unordered_map> // std::unordered_map을 사용하기 위해 필요
#include <vector>   // 개별 체이닝 구현을 위해 필요
#include <list>     // 개별 체이닝 구현을 위해 필요 (연결 리스트)

// --- 사용자 정의 해시 테이블 (개별 체이닝 방식) ---
template <typename Key, typename Value>
class MyHashTable {
private:
    std::vector<std::list<std::pair<Key, Value>>> table;
    int capacity;
    int current_size;

    // 간단한 해시 함수 (정수 키를 위한 모듈로 연산)
    // 실제 해시 함수는 std::hash를 사용하거나 더 복잡하게 구현해야 합니다.
    size_t hashFunction(const Key& key) const {
        // std::hash를 사용하여 다양한 타입의 키를 해싱할 수 있습니다.
        return std::hash<Key>{}(key) % capacity;
    }

public:
    MyHashTable(int cap) : capacity(cap), current_size(0) {
        table.resize(capacity);
    }

    // 값 삽입
    void insert(const Key& key, const Value& value) {
        size_t index = hashFunction(key);
        // 이미 키가 존재하는지 확인하고 업데이트
        for (auto& pair : table[index]) {
            if (pair.first == key) {
                pair.second = value; // 값 업데이트
                std::cout << "Updated key '" << key << "' with value '" << value << "'" << std::endl;
                return;
            }
        }
        // 키가 존재하지 않으면 새로운 쌍 추가
        table[index].push_back({key, value});
        current_size++;
        std::cout << "Inserted '" << key << "': '" << value << "'" << std::endl;
    }

    // 값 검색
    // const 참조로 반환하여 값을 수정할 수 있도록 하거나, 복사본 반환 또는 포인터 반환 고려
    Value* search(const Key& key) {
        size_t index = hashFunction(key);
        for (auto& pair : table[index]) {
            if (pair.first == key) {
                return &pair.second; // 값의 포인터 반환
            }
        }
        return nullptr; // 찾지 못하면 nullptr 반환
    }

    // 값 삭제
    void remove(const Key& key) {
        size_t index = hashFunction(key);
        auto& bucket = table[index];
        for (auto it = bucket.begin(); it != bucket.end(); ++it) {
            if (it->first == key) {
                bucket.erase(it);
                current_size--;
                std::cout << "Removed key '" << key << "'" << std::endl;
                return;
            }
        }
        std::cout << "Key '" << key << "' not found for removal." << std::endl;
    }

    // 현재 해시 테이블의 요소 수
    int size() const {
        return current_size;
    }

    // 해시 테이블 내용 출력
    void display() const {
        std::cout << "\n--- Hash Table Contents ---" << std::endl;
        for (int i = 0; i < capacity; ++i) {
            std::cout << "Bucket " << i << ": ";
            if (table[i].empty()) {
                std::cout << "[Empty]";
            } else {
                for (const auto& pair : table[i]) {
                    std::cout << "[" << pair.first << ": " << pair.second << "] ";
                }
            }
            std::cout << std::endl;
        }
        std::cout << "---------------------------" << std::endl;
    }
};


int main() {
    // --- std::unordered_map 사용 예시 ---
    std::cout << "--- std::unordered_map (C++ 표준 라이브러리) ---" << std::endl;
    std::unordered_map<std::string, int> ageMap;

    // 삽입 (insert 또는 [] 연산자 사용)
    ageMap["Alice"] = 30;
    ageMap["Bob"] = 25;
    ageMap["Charlie"] = 35;
    ageMap["Alice"] = 31; // 기존 키의 값 업데이트

    std::cout << "Alice's age: " << ageMap["Alice"] << std::endl; // 검색

    // 키 존재 여부 확인
    if (ageMap.count("Bob")) {
        std::cout << "Bob is in the map." << std::endl;
    }

    // 순회
    std::cout << "Map contents:" << std::endl;
    for (const auto& pair : ageMap) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    // 삭제
    ageMap.erase("Charlie");
    std::cout << "After deleting Charlie, map size: " << ageMap.size() << std::endl;

    if (ageMap.find("Charlie") == ageMap.end()) {
        std::cout << "Charlie is no longer in the map." << std::endl;
    }

    // --- 사용자 정의 해시 테이블 예시 ---
    std::cout << "\n--- 사용자 정의 해시 테이블 (개별 체이닝) ---" << std::endl;
    MyHashTable<std::string, std::string> myDictionary(10); // 크기 10의 해시 테이블

    myDictionary.insert("apple", "사과");
    myDictionary.insert("banana", "바나나");
    myDictionary.insert("cherry", "체리");
    myDictionary.insert("grape", "포도"); // 충돌 발생 가능성 있음 (해시 함수에 따라)
    myDictionary.insert("apple", "빨간 사과"); // 값 업데이트

    myDictionary.display();

    std::string* value = myDictionary.search("banana");
    if (value) {
        std::cout << "Found 'banana': " << *value << std::endl;
    } else {
        std::cout << "Not found 'banana'." << std::endl;
    }

    value = myDictionary.search("kiwi");
    if (value) {
        std::cout << "Found 'kiwi': " << *value << std::endl;
    } else {
        std::cout << "Not found 'kiwi'." << std::endl;
    }

    myDictionary.remove("cherry");
    myDictionary.display();

    myDictionary.remove("orange"); // 없는 키 삭제 시도

    std::cout << "Current size of custom hash table: " << myDictionary.size() << std::endl;

    return 0;
}
```

### Python에서의 해시 테이블 (딕셔너리)

Python에서는 내장 자료형인 \*\*`dict` (딕셔너리)\*\*가 해시 테이블로 구현되어 있습니다. `dict`는 매우 효율적이며, 키-값 쌍을 저장하고 관리하는 데 최적화되어 있습니다.

```python
# --- Python 딕셔너리 (Hash Table) 사용 예시 ---
print("--- Python 딕셔너리 (Hash Table) ---")

# 1. 딕셔너리 생성
my_dict = {
    "apple": "사과",
    "banana": "바나나",
    "cherry": "체리"
}
print(f"초기 딕셔너리: {my_dict}")

# 2. 값 삽입 또는 업데이트
my_dict["grape"] = "포도" # 새로운 키-값 쌍 추가
my_dict["apple"] = "빨간 사과" # 기존 키의 값 업데이트
print(f"삽입/업데이트 후 딕셔너리: {my_dict}")

# 3. 값 검색
print(f"apple의 값: {my_dict['apple']}")
print(f"banana의 값 (get() 사용): {my_dict.get('banana')}")
print(f"없는 키의 값 (get() 사용): {my_dict.get('kiwi', '없음')}") # '없음'은 기본값

# 4. 키 존재 여부 확인
if "cherry" in my_dict:
    print("'cherry' 키가 딕셔너리에 있습니다.")
if "orange" not in my_dict:
    print("'orange' 키는 딕셔너리에 없습니다.")

# 5. 값 삭제
del my_dict["banana"] # 키를 사용하여 삭제
print(f"banana 삭제 후 딕셔너리: {my_dict}")

# pop() 메소드를 사용하여 삭제 및 값 반환
popped_value = my_dict.pop("cherry")
print(f"cherry 삭제 후 딕셔너리: {my_dict}, 삭제된 값: {popped_value}")

# 6. 딕셔너리 순회
print("\n딕셔너리 순회:")
for key, value in my_dict.items(): # 키와 값을 함께 순회
    print(f"키: {key}, 값: {value}")

print("키만 순회:")
for key in my_dict.keys():
    print(f"키: {key}")

print("값만 순회:")
for value in my_dict.values():
    print(f"값: {value}")

# 7. 딕셔너리 크기
print(f"딕셔너리 크기: {len(my_dict)}")

# 8. 모든 요소 삭제
my_dict.clear()
print(f"clear() 후 딕셔너리: {my_dict}")
```