## 배열 (Array)

배열은 가장 기본적인 자료구조 중 하나로, 동일한 타입의 데이터들을 메모리 상에 연속적으로 저장하는 선형(linear) 자료구조입니다. 각 데이터는 인덱스(index) 또는 첨자(subscript)를 통해 접근할 수 있으며, 일반적으로 첫 번째 요소의 인덱스는 0부터 시작합니다.

### 특징

  * **연속적인 메모리 할당:** 배열의 모든 요소는 메모리 상에서 서로 인접하게 저장됩니다. 이로 인해 인덱스를 통한 직접 접근(Direct Access)이 가능하며, 특정 요소의 주소를 빠르게 계산할 수 있습니다.
  * **고정된 크기 (일반적으로):** 대부분의 프로그래밍 언어에서 배열은 선언 시 크기가 고정됩니다. 즉, 한 번 생성된 배열의 크기는 실행 중에 변경할 수 없습니다. (단, 동적 배열의 경우 예외)
  * **동일한 데이터 타입:** 배열은 동일한 타입의 데이터만을 저장할 수 있습니다. 예를 들어, 정수형 배열은 정수만, 문자열 배열은 문자열만 저장할 수 있습니다.
  * **빠른 접근 속도:** 인덱스를 알고 있다면 $O(1)$의 시간 복잡도로 특정 요소에 접근할 수 있습니다. 이는 메모리 주소를 직접 계산할 수 있기 때문입니다.
  * **삽입 및 삭제의 비효율성:** 배열 중간에 요소를 삽입하거나 삭제할 경우, 그 이후의 모든 요소들을 이동시켜야 하므로 $O(N)$의 시간 복잡도가 발생합니다.

### 장점

  * 인덱스를 이용한 빠른 접근 ($O(1)$)
  * 간단한 구조와 구현
  * 캐시 지역성(Cache Locality)으로 인한 성능 이점 (연속적인 메모리 접근)

### 단점

  * 고정된 크기로 인한 유연성 부족
  * 삽입 및 삭제 연산의 비효율성
  * 메모리 낭비 가능성 (선언된 크기만큼 항상 사용하지 않을 경우)

### 사용 예시

  * 성적 관리 시스템에서 학생들의 점수 저장
  * 이미지 처리에서 픽셀 데이터 저장
  * 행렬 연산

### C++에서의 배열

C++에서는 정적 배열(Static Array)과 동적 배열(Dynamic Array)을 사용할 수 있습니다. `std::vector`는 동적 배열의 기능을 제공하는 컨테이너입니다.

```cpp
#include <iostream> // 입출력을 위해 필요
#include <vector>   // std::vector를 사용하기 위해 필요

int main() {
    // 1. 정적 배열 (Static Array)
    // 크기가 5인 정수형 배열 선언 및 초기화
    int staticArray[5] = {10, 20, 30, 40, 50};

    std::cout << "--- 정적 배열 ---" << std::endl;
    // 배열 요소 접근 및 출력
    for (int i = 0; i < 5; ++i) {
        std::cout << "staticArray[" << i << "] : " << staticArray[i] << std::endl;
    }

    // 특정 인덱스 요소 변경
    staticArray[2] = 35;
    std::cout << "staticArray[2] 변경 후 : " << staticArray[2] << std::endl;

    // 2. 동적 배열 (Dynamic Array) - std::vector 사용
    // std::vector는 크기가 가변적인 배열처럼 동작
    std::vector<int> dynamicArray;

    std::cout << "\n--- 동적 배열 (std::vector) ---" << std::endl;
    // 요소 추가 (뒤에 삽입)
    dynamicArray.push_back(100);
    dynamicArray.push_back(200);
    dynamicArray.push_back(300);

    // 현재 크기 출력
    std::cout << "dynamicArray의 현재 크기 : " << dynamicArray.size() << std::endl;

    // 요소 접근 및 출력
    for (size_t i = 0; i < dynamicArray.size(); ++i) {
        std::cout << "dynamicArray[" << i << "] : " << dynamicArray[i] << std::endl;
    }

    // 특정 인덱스 요소 변경
    dynamicArray[1] = 250;
    std::cout << "dynamicArray[1] 변경 후 : " << dynamicArray[1] << std::endl;

    // 중간에 요소 삽입 (비효율적일 수 있음)
    // 이터레이터를 사용하여 두 번째 위치(인덱스 1)에 150 삽입
    dynamicArray.insert(dynamicArray.begin() + 1, 150);
    std::cout << "\n--- 150 삽입 후 dynamicArray ---" << std::endl;
    for (size_t i = 0; i < dynamicArray.size(); ++i) {
        std::cout << "dynamicArray[" << i << "] : " << dynamicArray[i] << std::endl;
    }

    // 요소 삭제 (뒤에서 삭제)
    dynamicArray.pop_back();
    std::cout << "\n--- 마지막 요소 삭제 후 dynamicArray ---" << std::endl;
    for (size_t i = 0; i < dynamicArray.size(); ++i) {
        std::cout << "dynamicArray[" << i << "] : " << dynamicArray[i] << std::endl;
    }

    // 중간 요소 삭제 (비효율적일 수 있음)
    // 이터레이터를 사용하여 세 번째 위치(인덱스 2) 요소 삭제
    dynamicArray.erase(dynamicArray.begin() + 2);
    std::cout << "\n--- 인덱스 2 요소 삭제 후 dynamicArray ---" << std::endl;
    for (size_t i = 0; i < dynamicArray.size(); ++i) {
        std::cout << "dynamicArray[" << i << "] : " << dynamicArray[i] << std::endl;
    }

    return 0;
}
```

### Python에서의 배열 (리스트)

Python에서는 내장 자료형인 `list`가 배열의 기능을 유연하게 제공합니다. Python의 `list`는 내부적으로 동적 배열처럼 동작하며, 다양한 타입의 데이터를 저장할 수 있습니다.

```python
# 1. 리스트 (Python의 동적 배열) 생성
my_list = [10, 20, 30, 40, 50]
print("--- 초기 리스트 ---")
print(my_list)

# 2. 요소 접근
print(f"my_list[0]: {my_list[0]}")
print(f"my_list[2]: {my_list[2]}")
print(f"my_list[-1]: {my_list[-1]} (음수 인덱스는 뒤에서부터 접근)")

# 3. 요소 변경
my_list[2] = 35
print(f"my_list[2] 변경 후: {my_list}")

# 4. 요소 추가 (append: 리스트 끝에 추가)
my_list.append(60)
print(f"60 추가 후: {my_list}")

# 5. 요소 삽입 (insert: 특정 인덱스에 삽입)
my_list.insert(1, 15) # 인덱스 1에 15 삽입
print(f"15 삽입 후: {my_list}")

# 6. 요소 삭제 (remove: 값으로 삭제, 없으면 오류)
my_list.remove(35)
print(f"35 삭제 후: {my_list}")

# 7. 요소 삭제 (pop: 인덱스로 삭제, 기본적으로 마지막 요소 삭제 후 반환)
popped_value = my_list.pop()
print(f"마지막 요소 {popped_value} 삭제 후: {my_list}")

popped_value_at_index = my_list.pop(1) # 인덱스 1의 요소 삭제
print(f"인덱스 1의 요소 {popped_value_at_index} 삭제 후: {my_list}")

# 8. 리스트 길이 (요소 개수)
print(f"리스트의 길이: {len(my_list)}")

# 9. 슬라이싱 (부분 리스트 추출)
sub_list = my_list[1:3] # 인덱스 1부터 3 전까지 (1, 2)
print(f"my_list[1:3] 슬라이싱: {sub_list}")

# 10. 리스트 반복
print("--- 리스트 반복 ---")
for item in my_list:
    print(item)
```