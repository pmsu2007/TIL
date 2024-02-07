# Binary Search

이분 탐색(Binary Search)는 <u>**정렬된 배열**</u>에서 **탐색 범위를 좁혀가면서 <u>특정 값을 찾아나가는**</u> 알고리즘이다.

## 이분 탐색 과정

1. 배열의 중간 값을 선택하여 찾고자 하는 값과 비교한다.
2. 만약 중간 값이 찾고자 하는 값 보다 **크다면 중간 값 왼쪽으로 탐색 범위를 좁히고**, 중간 값이 찾고자 하는 값 보다 **작다면 중간 값 오른쪽으로 탐색 범위를 좁힌다.**
3. 중간 값과 찾고자 하는 값이 일치할 때 까지 이 과정을 반복한다.

## 이분 탐색 소스 코드

### 1. `while`문을 이용하는 이분 탐색
```java
public static int binarySearch(int[] arr, int target) {
    int left = 0;
    int right = arr.length - 1;

    while (left <= right) {
        int mid = (left + right) / 2;

        if (arr[mid] == target) {
            return mid;
        }

        // 찾고자하는 값이 중간 값 보다 클 때
        if (arr[mid] < target) {
            left = mid + 1;
        }

        // 찾고자하는 값이 중간 값 보다 작을 때
        if (arr[mid] > target) {
            right = mid - 1;
        }
    }

    // 못 찾은 경우
    return -1; 
}
```

### 2. 재귀 함수를 이용하는 이분 탐색
```java
public static int binarySearch(int[] arr, int target, int left, int right) {
    if (left <= right) {
        int mid = (left + right) / 2;

        if (arr[mid] == target) {
            return mid;
        }

        if (arr[mid] > target) {
            return binarySearch(arr, target, left, mid - 1);
        }

        if (arr[mid] < target) {
            return binarySearch(arr, target, mid + 1, right);
        }
    }

    return -1;
}
```