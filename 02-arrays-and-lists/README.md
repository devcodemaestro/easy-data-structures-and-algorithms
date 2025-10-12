## 배열기초

배열이란 **같은 타입의 데이터**를 **연속적인 메모리 공간에 저장**하는 자료구조다.이로 인해 메모리 효율성이 높고, 캐싱 및 요소 접근이 빠르다.

배열 생성은 시간복잡도와 공간복잡도가 모두 O(n)이다.

### 조회(Access) / 수정(Update)

- 배열 크기와 상관없이 인덱스로 바로 값을 찾아 조회나 수정할 수 있다.

- 따라서 시간복잡도와 공간복잡도는 O(1)이다.

  ```python
  # 생성
  arr = [27, 36, 45, 44, 21, 24, 82, 11]

  # 조회
  print(arr[3])
  # 44

  # 수정
  arr[5] = 16

  print(arr)
  # [27, 36, 45, 44, 21, 16, 82, 11]
  ```

  ```java
  public class ArrayExample {
    public static void main(String[] args) {
      // 생성
      int[] arr = {27, 36, 45, 44, 21, 24, 82, 11};
      // 조회
      System.out.println(arr[3]);
      // 44

      // 수정
      arr[5] = 16;
    }
  }
  ```

### 파이썬과 자바 배열의 차이

파이썬과 자바스크립트의 배열은 엄밀히 말하면 리스트다. 서로 다른 데이터 타입을 참조자료형으로 하나로 담을 수 있기 때문이다.

### Linear Search(선형 탐색)

- 배열 모든 요소를 순회하는 경우도 배열의 길이에 따라 연산 횟수가 비례하므로 O(n)의 시간 복잡도를 갖는다.

- 특정 값이 제일 첫 인덱스에 있을 수도 있지만 가장 마지막에 있을 수도 있다. 시간 복잡도는 항상 가장 오래 걸리는 경우(최악의 상황)에 맞춰 계산한다.

  ```python
  # Linear Search. 배열 순회 중 특정 값을 찾으면 종료하는 형태
  # 파이썬 코드
  arr = [27, 36, 45, 44, 21, 16, 82, 11]
  for i in range(len(arr)):
      if arr[i] == 45:
          print(i)
          break
  ```

  ```java
  // 자바코드
  public class ArraySearchTraverse {
    public static void main(String[] args) {
        int[] arr = {27, 36, 45, 44, 21, 16, 82, 11};

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == 45) {
                System.out.println(i);
                break;
            }
        }
    }
  }
  ```

### Traverse Array(배열 순회 또는 배열 전체 탐색)

- 선형 탐색과 마찬가지로 배열을 끝까지 순회해야 하므로 O(n)의 시간 복잡도를 갖는다.

  ```python
  # Traverse Array. 파이썬 코드
  # 배열을 끝까지 순회해야만 함. 반복 출력이나 합계 구하기 같은 경우.
  arr = [27, 36, 45, 44, 21, 16, 82, 11]
  for val in arr:
      print(val)
  ```

  ```java
  // 자바코드
  public class ArraySearchTraverse {
    public static void main(String[] args) {
      for (int i = 0; i < arr.length; i++) {
          System.out.println(arr[i]);
      }
    }
  }
  ```

## 정적 배열과 동적 배열

배열은 기본적으로 크기가 고정된다. 따라서 요소를 삭제하거나 추가하면, 나머지 요소들이 앞으로 당겨지거나 뒤로 밀리는 **추가 이동이 발생**하다.

### 삭제(Delete) / 추가(Insert)

- 특정 인덱스의 값을 삭제하거나 추가시 나머지 요소들을 하나씩 당기거나 밀어내는 추가 연산을 반드시 진행하게 됨. 따라서 O(n)의 시간 복잡도를 갖는다.

  ```python
  # 삽입을 위한 파이썬 코드
  arr = [27, 36, 45, 44, 21, 16, 82, 11]

  # 파이썬은 동적배열이기 때문에 삭제나 추가시 자동으로 길이가 변경됨
  # 삭제
  del arr[5]

  print(arr)
  # [27, 36, 45, 44, 21, 82, 11]

  # 추가.
  arr.insert(1, 33)

  print(arr)
  # [27, 33, 36, 45, 44, 21, 82, 11]
  ```

  ```java
  // 삽입을 위한 자바코드
  import java.util.Arrays;

  public class InsertIntoArray {
    public static void main(String[] args) {
      // 길이가 고정된 기존 배열
      int[] original = {27, 33, 36, 45, 44, 21, 82, 11};
      // 기존 배열보다 크기가 하나만큼 더 큰 배열을 새로 생성
      int[] result = new int[original.length + 1];
      // 삽입할 인덱스 번호
      int insertIndex = 2;
      // 삽입할 값
      int insertValue = 10;
      // 반복해서 추가할 인덱스보다 앞의 요소들을 새 배열의 같은 인덱스로 복사
      for (int i = 0; i < insertIndex; i++) {
        result[i] = original[i];
      }
      // 추가할 값을 새 배열의 목표 인덱스에 삽입
      result[insertIndex] = insertValue;
      // 나머지 값을을 반복해서 새 배열에 기존 인덱스보다 하나 뒤에 자리에 삽입
      for (int i = insertIndex; i < original.length; i++) {
        result[i + 1] = original[i];
      }

      System.out.println(Arrays.toString(result));
      // [27, 33, 10, 36, 45, 44, 21, 82, 11]
    }
  }
  ```

### 자바로 동적 배열 직접 구현해보기

- 재사용 가능한 자바 클래스로 직접 구현하는 코드

  ````java
  // 자바 코드
  import java.util.Arrays;

      class DynamicArray {
        // 크기가 8인 빈 정수 배열로 초기화
        private int[] data = new int[8];
        // 실제 값이 들어있는 부분의 크기를 나타낼 변수
        private int size = 0;

        // 값을 추가하는 메소드
        public void add(int value) {
          // 배열에 추가공간 확보를 위해 ensureCapaticy 메소드를 먼저 실행.
          ensureCapacity();
          // 실제 값인 size를 통해 추가 인덱스에 값 추가.
          data[size++] = value;
        }

        // 주어진 인덱스에 값을 추가하는 메소드
        public void insert(int index, int value) {
          // 배열에 추가공간 확보를 위해 ensureCapaticy 메소드를 먼저 실행.
          ensureCapacity();
            // 추가할 인덱스 뒤의 요소들을 하나씩 뒤로 옮김
            for (int i = size; i > index; i--) {
              data[i] = data[i - 1];
            }
          // 인덱스에 값 추가
          data[index] = value;
          // 추가한 만큼 사이즈도 늘림
          size++;
        }

        // 공간이 부족할 시 더 큰 배열을 만드는 메소드
        private void ensureCapacity() {
          // size의 값이 data배열의 크기와 같거나 크면
          if (size >= data.length) {
            // 기존 배열의 2배 크기 newData 배열을 생성
            int[] newData = new int[data.length * 2];
              // 값을 반복해서 하나씩 newData로 옮김
              for (int i = 0; i < size; i++) {
                newData[i] = data[i];
              }
            // data를 크기를 넓힌 newData로 치환
            data = newData;
          }
        }

        public String toString() {
          return Arrays.toString(Arrays.copyOf(data, size));
        }
      }
      // DynamicArray 클래스 생성완료

      public class InsertExample {
        public static void main(String[] args) {
          // DynamicArray 인스턴스 생성. 8개의 빈 공간 배열 생성됨
          DynamicArray arr = new DynamicArray();
          int[] initial = {27, 33, 36, 45, 44, 21, 82, 11};
          // 인스턴스에 생성한 배열의 값을 넣어줌. 총 8개.
          for (int num : initial) arr.add(num);

          // 2번 인덱스에 10의 값을 넣으려고 함.
          // insert 메소드에서 ensureCapacity()가 실행되며 공간이 2배 늘어나고 값 추가됨.
          arr.insert(2, 10);

          // 내부 공간은 16이 되고 값은 9개가 되어 아래의 결과가 출력됨
          System.out.println(arr);
          // [27, 33, 10, 36, 45, 44, 21, 82, 11]
        }
      }
      ```

      ```java
      // 자바 코드
      import java.util.Arrays;

      public class ArrayModify {
        public static void main(String[] args) {
          // 자바의 숫자 배열에 'null' 값을 넣기 위해 자바 기본 자료형인 int가 아니라 클래스인 Integer로 배열을 만들어야 한다.
          Integer[] arr = {27, 36, 45, 44, 21, 16, 82, 11};

          // 삭제시 뒤의 배열을 앞으로 당기는 코드
          for (int i = 5; i < arr.length - 1; i++) {
              arr[i] = arr[i + 1];
          }
          arr[arr.length - 1] = null;

          System.out.println(Arrays.toString(arr));
          // [27, 36, 45, 44, 21, 82, 11, null]

          // 추가시 뒤의 배열을 +1 인덱스 미는 코드
          for (int i = arr.length - 1; i > 1; i--) {
              arr[i] = arr[i - 1];
          }
          arr[1] = 33;

          System.out.println(Arrays.toString(arr));
          // [27, 33, 36, 45, 44, 21, 82, 11]
        }
      }
      ```
  ````

- 자바 내장 라이브러리 ArrayList를 사용하면 동적배열을 만들 수 있다.
- 주류 언어들에서 동적 배열을 제공하기 때문에 원리만 이해하고 있으면 된다.

  ```java
  import java.util.ArrayList;
  import java.util.Arrays;

  public class Main {
      public static void main(String[] args) {
          ArrayList<Integer> list = new ArrayList<>(
              Arrays.asList(27, 33, 36, 45, 44, 21, 82, 11)
          );

          list.add(2, 10);

          System.out.println(list);
          // Output: [27, 33, 10, 36, 45, 44, 21, 82, 11]
      }
  }
  ```

## 2차원 배열

n행과 m열의 배열을 생성하는 작업은 한 줄(row)에 m개의 의자를 놓고, 그런 줄이 n줄 있는 구조다. 행이 n개, 각 행에 열이 m개 존재한다. 따라서 시간 복잡도와 공간 복잡도 모두 n\*m이 된다.

배열 안에 다수 배열들이 들어있는 구조가 된다.

### 조회(Access) / 수정(Update)

- 배열 크기와 상관없이 인덱스로 바로 값을 찾아 조회나 수정할 수 있다.

- 따라서 시간복잡도와 공간복잡도는 O(1)이다.

  ```python
  arr = [[1, 2, 3, 4],
        [5, 6, 7, 8],
        [9,10,11,12]]

  print(arr[1][2]) # 7

  arr[1][2] = 99
  print(arr[1][2]) # 99
  ```

  ```java
  public class Array2DExample {
    public static void main(String[] args) {
      int[][] arr = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9,10,11,12}
      };

      System.out.println(arr[1][2]);  // 7

      arr[1][2] = 99;
      System.out.println(arr[1][2]);  // 99
    }
  }
  ```

### Search Element

- 찾는 값이 나올 때까지 12개의 요소들을 하나하나 살펴보는 것.
- 2차원 배열의 Linear Search라 볼 수 있다.

### Traverse row

- 열 방향(가로)으로 m개 요소를 순회하므로 시간복잡도는 O(m)

```js
for (let j = 0; j < m; j++) {
  console.log(arr[i][j]); // i는 고정, 한 행의 모든 열 순회
}
```

### Traverse Column

- 행 방향(세로)으로 n개 요소를 순회하므로 시간복잡도는 O(n)

```js
for (let i = 0; i < n; i++) {
  console.log(arr[i][j]); // j는 고정, 한 열의 모든 행 순회
}
```

### Traverse All

- 모든 행과 열을 순회하므로 시간 복잡도는 O(n\*m)

```js
for (let i = 0; i < n; i++) {
  // 행 순회
  for (let j = 0; j < m; j++) {
    // 열 순회
    console.log(arr[i][j]);
  }
}
```

### 코드 예시

- 파이썬 코드 예시

  ```python
  # 배열 생성 및 초기화
  arr = [[1, 2, 3, 4],
        [5, 6, 7, 8],
        [9,10,11,12]]

  # 조회
  print(arr[1][2]) # 7

  # 수정
  arr[1][2] = 99
  print(arr[1][2]) # 99

  # 원하는 값 조회
  for i in range(3):
      for j in range(4):
          if arr[i][j] == 10:
              print((i, j))
              # (2, 1)

  # 인덱스가 1인 행을 순회
  for val in arr[1]:
      print(val, end=' ')
      # 5 6 99 8

  # 인덱스가 2인 열을 순회
  for i in range(3):
      print(arr[i][2], end=' ')
      # 3 99 11

  # 전체 순회
  for row in arr:
      for val in row:
          print(val, end=' ')
          # 1 2 3 4 5 6 99 8 9 10 11 12
  ```

- 자바코드 예시

  ```java
  public class Array2DExample {
    public static void main(String[] args) {
      // 배열 생성 및 초기화
      int[][] arr = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9,10,11,12}
      };

      // 조회
      System.out.println(arr[1][2]);  // 7

      // 수정
      arr[1][2] = 99;
      System.out.println(arr[1][2]);  // 99

      // 원하는 값 조회
      for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
          if (arr[i][j] == 10) {
            System.out.println("(" + i + ", " + j + ")");
            // (2, 1)
          }
        }
      }

      // 인덱스가 1인 행을 순회
      for (int j = 0; j < 4; j++) {
        System.out.print(arr[1][j] + " ");
        // 5 6 99 8
      }
      System.out.println();

      // 인덱스가 2인 열을 순회
      for (int i = 0; i < 3; i++) {
        System.out.print(arr[i][2] + " ");
        // 3 99 11
      }
      System.out.println();

      // 전체 순회
      for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
          System.out.print(arr[i][j] + " ");
          // 1 2 3 4 5 6 99 8 9 10 11 12
        }
      }
    }
  }
  ```

### 2차원 배열의 내부적 구현 방식

C나 C++ 같은 언어에서는 다차원 배열이 실제 메모리 내에서도 연속된 공간에 배치된다.
<br>따라서 2차원 배열의 크기 전체가 고정되어 있다.

자바와 같은 언어에서는 여러 위치의 주소값들을 배열 내에 요소로 저장해 다차원 배열을 만든다.

따라서 아래와 같이 내부 배열의 크기가 다른 배열을 만들 수 있다.

```python
arr = [
    [1, 2],
    [3, 4, 5],
    [6]
]
```

## 단일 연결 리스트
