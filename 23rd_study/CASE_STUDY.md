
-----

# 프로그래머스 문제 풀이: 정수 내림차순으로 배치하기 (Python)

**문제 설명:**
함수 `solution`은 정수 `n`을 매개변수로 받습니다. `n`의 각 자릿수를 큰 것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를 들어, `n`이 `118372`면 `873211`을 리턴하면 됩니다.

**제한 조건:**

  * `n`은 1 이상 8,000,000,000 이하인 자연수입니다.

-----

## 문제 해결 전략

1.  **정수를 문자열로 변환:** 정수 `n`은 각 자릿수를 개별적으로 다루기 어렵습니다. 따라서 먼저 문자열로 변환하여 각 자릿수를 쉽게 접근할 수 있도록 합니다.
2.  **문자열을 리스트로 변환:** 문자열 상태에서는 정렬 함수를 적용하기 어려우므로, 각 문자를 요소로 하는 리스트로 변환합니다. (예: "118372" -\> `['1', '1', '8', '3', '7', '2']`)
3.  **리스트 정렬:** 변환된 문자(숫자) 리스트를 내림차순으로 정렬합니다. 이때 `sort()` 함수 대신 우리가 직접 구현한 정렬 함수(버블, 삽입, 선택)를 사용합니다.
4.  **리스트를 문자열로 다시 결합:** 정렬된 문자 리스트를 하나의 문자열로 다시 합칩니다.
5.  **문자열을 정수로 변환:** 최종 문자열을 다시 정수형으로 변환하여 반환합니다.

-----

## 1\. 버블 정렬을 이용한 풀이

### 1.1. 버블 정렬 기반 슈도코드

```pseudocode
FUNCTION solution(n)
    # 1. 정수를 문자열로 변환
    s = CONVERT n TO STRING # 예: "118372"

    # 2. 문자열을 문자 리스트로 변환
    char_list = CONVERT s TO LIST OF CHARACTERS # 예: ['1', '1', '8', '3', '7', '2']

    # 3. 버블 정렬 함수 구현 및 적용 (내림차순)
    #    (이 부분은 이전에 작성한 BubbleSort 함수와 유사하나, 내림차순으로 변경)
    n_len = LENGTH of char_list
    FOR i FROM 0 TO n_len - 2 DO
        FOR j FROM 0 TO n_len - 2 - i DO
            # 현재 문자가 다음 문자보다 작으면 (내림차순 정렬을 위해)
            IF char_list[j] < char_list[j+1] THEN
                SWAP char_list[j] AND char_list[j+1]
            END IF
        END FOR
    END FOR

    # 4. 정렬된 리스트를 문자열로 다시 결합
    sorted_s = JOIN char_list INTO SINGLE STRING # 예: "873211"

    # 5. 문자열을 정수로 변환하여 반환
    RETURN CONVERT sorted_s TO INTEGER

END FUNCTION
```

### 1.2. 버블 정렬 기반 파이썬 코드

```python
def bubble_sort_descending(arr):
    """
    주어진 리스트를 버블 정렬 방식으로 내림차순 정렬하는 함수
    """
    n = len(arr)
    for i in range(n - 1):
        for j in range(n - 1 - i):
            # 내림차순 정렬: 현재 요소가 다음 요소보다 작으면 위치를 바꿉니다.
            if arr[j] < arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def solution_bubble_sort(n):
    # 1. 정수를 문자열로 변환 (각 자릿수를 다루기 위함)
    s = str(n)

    # 2. 문자열을 문자 리스트로 변환
    char_list = list(s) # 예: "118372" -> ['1', '1', '8', '3', '7', '2']

    # 3. 리스트를 내림차순으로 버블 정렬 (직접 구현한 함수 사용)
    sorted_char_list = bubble_sort_descending(char_list)

    # 4. 정렬된 문자 리스트를 다시 하나의 문자열로 결합
    # ['8', '7', '3', '2', '1', '1'] -> "873211"
    sorted_s = "".join(sorted_char_list)

    # 5. 문자열을 정수로 변환하여 반환
    return int(sorted_s)

# 테스트 케이스
print(f"버블 정렬 풀이 (118372): {solution_bubble_sort(118372)}") # 기대값: 873211
print(f"버블 정렬 풀이 (12345): {solution_bubble_sort(12345)}")   # 기대값: 54321
```

-----

## 2\. 삽입 정렬을 이용한 풀이

### 2.1. 삽입 정렬 기반 슈도코드

```pseudocode
FUNCTION solution(n)
    # 1. 정수를 문자열로 변환
    s = CONVERT n TO STRING

    # 2. 문자열을 문자 리스트로 변환
    char_list = CONVERT s TO LIST OF CHARACTERS

    # 3. 삽입 정렬 함수 구현 및 적용 (내림차순)
    #    (이전에 작성한 InsertionSort 함수와 유사하나, 내림차순으로 변경)
    n_len = LENGTH of char_list
    FOR i FROM 1 TO n_len - 1 DO
        key = char_list[i]
        j = i - 1
        # key보다 작은 요소들은 오른쪽으로 한 칸씩 밀어냄 (내림차순 정렬을 위해)
        WHILE j >= 0 AND char_list[j] < key DO
            char_list[j+1] = char_list[j]
            j = j - 1
        END WHILE
        char_list[j+1] = key
    END FOR

    # 4. 정렬된 리스트를 문자열로 다시 결합
    sorted_s = JOIN char_list INTO SINGLE STRING

    # 5. 문자열을 정수로 변환하여 반환
    RETURN CONVERT sorted_s TO INTEGER

END FUNCTION
```

### 2.2. 삽입 정렬 기반 파이썬 코드

```python
def insertion_sort_descending(arr):
    """
    주어진 리스트를 삽입 정렬 방식으로 내림차순 정렬하는 함수
    """
    n = len(arr)
    for i in range(1, n):
        key = arr[i]
        j = i - 1
        # 내림차순 정렬: key가 들어갈 위치를 찾기 위해,
        # key보다 작은 요소들을 오른쪽으로 한 칸씩 이동시킵니다.
        while j >= 0 and arr[j] < key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

def solution_insertion_sort(n):
    s = str(n)
    char_list = list(s)
    
    # 리스트를 내림차순으로 삽입 정렬
    sorted_char_list = insertion_sort_descending(char_list)

    sorted_s = "".join(sorted_char_list)
    return int(sorted_s)

# 테스트 케이스
print(f"삽입 정렬 풀이 (118372): {solution_insertion_sort(118372)}") # 기대값: 873211
print(f"삽입 정렬 풀이 (12345): {solution_insertion_sort(12345)}")   # 기대값: 54321
```

-----

## 3\. 선택 정렬을 이용한 풀이

### 3.1. 선택 정렬 기반 슈도코드

```pseudocode
FUNCTION solution(n)
    # 1. 정수를 문자열로 변환
    s = CONVERT n TO STRING

    # 2. 문자열을 문자 리스트로 변환
    char_list = CONVERT s TO LIST OF CHARACTERS

    # 3. 선택 정렬 함수 구현 및 적용 (내림차순)
    #    (이전에 작성한 SelectionSort 함수와 유사하나, 내림차순으로 변경)
    n_len = LENGTH of char_list
    FOR i FROM 0 TO n_len - 2 DO
        # 현재 정렬되지 않은 부분에서 가장 큰 요소의 인덱스를 찾기 (내림차순이므로)
        max_idx = i

        FOR j FROM i + 1 TO n_len - 1 DO
            # 현재까지 찾은 가장 큰 요소보다 더 큰 요소를 발견하면
            IF char_list[j] > char_list[max_idx] THEN
                max_idx = j # max_idx를 그 요소의 인덱스로 업데이트
            END IF
        END FOR

        # 가장 큰 요소를 찾았으면, 현재 위치(i)의 요소와 가장 큰 요소(max_idx)의 위치를 바꿈
        SWAP char_list[i] AND char_idx[max_idx]
    END FOR

    # 4. 정렬된 리스트를 문자열로 다시 결합
    sorted_s = JOIN char_list INTO SINGLE STRING

    # 5. 문자열을 정수로 변환하여 반환
    RETURN CONVERT sorted_s TO INTEGER

END FUNCTION
```

### 3.2. 선택 정렬 기반 파이썬 코드

```python
def selection_sort_descending(arr):
    """
    주어진 리스트를 선택 정렬 방식으로 내림차순 정렬하는 함수
    """
    n = len(arr)
    for i in range(n - 1):
        # 내림차순 정렬: 현재 정렬되지 않은 부분에서 가장 큰 요소의 인덱스를 찾습니다.
        max_idx = i
        for j in range(i + 1, n):
            if arr[j] > arr[max_idx]: # 현재 요소가 max_idx의 요소보다 크면
                max_idx = j # max_idx 업데이트
        
        # 가장 큰 요소를 현재 위치(i)로 가져옵니다.
        arr[i], arr[max_idx] = arr[max_idx], arr[i]
    return arr

def solution_selection_sort(n):
    s = str(n)
    char_list = list(s)
    
    # 리스트를 내림차순으로 선택 정렬
    sorted_char_list = selection_sort_descending(char_list)

    sorted_s = "".join(sorted_char_list)
    return int(sorted_s)

# 테스트 케이스
print(f"선택 정렬 풀이 (118372): {solution_selection_sort(118372)}") # 기대값: 873211
print(f"선택 정렬 풀이 (12345): {solution_selection_sort(12345)}")   # 기대값: 54321
```

-----

## 결론

이 문제에서는 `n`의 최대값이 80억이므로 자릿수는 최대 10자리(8,000,000,000) 정도입니다. 즉, 리스트의 크기(N)가 **최대 10** 정도밖에 되지 않으므로, $O(N^2)$의 시간 복잡도를 가진 버블, 삽입, 선택 정렬로도 충분히 문제를 해결할 수 있습니다.

실제 코딩 테스트에서는 내장 `sort()` 함수를 사용하는 것이 훨씬 효율적이고 권장되지만, 이 과정을 통해 기본적인 정렬 알고리즘의 동작 원리와 슈도코드 작성, 그리고 파이썬으로의 구현 과정을 직접 경험해보는 것은 알고리즘 이해에 큰 도움이 될 것입니다.

---
