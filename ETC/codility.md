# Codility

별도의 코멘트가 없는 경우 스코어 100%인 풀이이다.

## Lesson 1 Iterations

### [BinaryGap](https://app.codility.com/programmers/lessons/1-iterations/binary_gap/)

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

```
function solution(N);
```

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [1..2,147,483,647].

#### 나의 풀이

```javascript
function solution(N) {
  const array = [];
  let quotient = N;

  while (quotient > 0) {
    array.unshift(quotient % 2);
    quotient = Math.floor(quotient / 2);
  }

  let maxZeroCount = 0;
  let currentZeroCount = 0;
  for (let i = 0; i < array.length; i++) {
    if (array[i] === 0) {
      currentZeroCount++;
    } else {
      if (maxZeroCount < currentZeroCount) {
        maxZeroCount = currentZeroCount;
      }
      currentZeroCount = 0;
    }
  }

  return maxZeroCount;
}
```

## Lesson2 Arrays

### [CyclicRotation](https://app.codility.com/programmers/lessons/2-arrays/cyclic_rotation/)

An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

```
class Solution { public int[] solution(int[] A, int K); }
```

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

```
A = [3, 8, 9, 7, 6]
K = 3
```

the function should return [9, 7, 6, 3, 8]. Three rotations were made:

```
[3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
[6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
[7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
```

For another example, given

```
A = [0, 0, 0]
K = 1
```

the function should return [0, 0, 0]

Given

```
A = [1, 2, 3, 4]
K = 4
```

the function should return [1, 2, 3, 4]

Assume that:

- N and K are integers within the range [0..100];
- each element of array A is an integer within the range [−1,000..1,000].

In your solution, focus on correctness. The performance of your solution will not be the focus of the assessment.

#### 나의 풀이

```javascript
function solution(A, K) {
  const remainder = K % A.length;
  const result = [];

  for (let i = 0; i < A.length; i++) {
    const index = (A.length - remainder + i) % A.length;
    result.push(A[index]);
  }

  return result;
}
```

### [OddOccurrencesInArray](https://app.codility.com/programmers/lessons/2-arrays/odd_occurrences_in_array/)

A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

```
A[0] = 9  A[1] = 3  A[2] = 9
A[3] = 3  A[4] = 9  A[5] = 7
A[6] = 9
```

- the elements at indexes 0 and 2 have value 9,
- the elements at indexes 1 and 3 have value 3,
- the elements at indexes 4 and 6 have value 9,
- the element at index 5 has value 7 and is unpaired.
  Write a function:

```
function solution(A);
```

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

```
A[0] = 9  A[1] = 3  A[2] = 9
A[3] = 3  A[4] = 9  A[5] = 7
A[6] = 9
```

the function should return 7, as explained in the example above.

Write an efficient algorithm for the following assumptions:

- N is an odd integer within the range [1..1,000,000];
- each element of array A is an integer within the range [1..1,000,000,000];
- all but one of the values in A occur an even number of times.

#### 나의 풀이

```javascript
function solution(A) {
  const map = new Map();

  for (let i = 0; i < A.length; i++) {
    const value = map.get(A[i]);
    if (value === undefined) {
      map.set(A[i], true);
    } else {
      map.delete(A[i]);
    }
  }

  return map.keys().next().value;
}
```

## Time Complexity

### [FrogJmp](https://app.codility.com/programmers/lessons/3-time_complexity/frog_jmp/)

A small frog wants to get to the other side of the road. The frog is currently located at position X and wants to get to a position greater than or equal to Y. The small frog always jumps a fixed distance, D.

Count the minimal number of jumps that the small frog must perform to reach its target.

Write a function:

```
function solution(X, Y, D);
```

that, given three integers X, Y and D, returns the minimal number of jumps from position X to a position equal to or greater than Y.

For example, given:

```
X = 10
Y = 85
D = 30
```

the function should return 3, because the frog will be positioned as follows:

- after the first jump, at position 10 + 30 = 40
- after the second jump, at position 10 + 30 + 30 = 70
- after the third jump, at position 10 + 30 + 30 + 30 = 100

Write an efficient algorithm for the following assumptions:

- X, Y and D are integers within the range [1..1,000,000,000];
- X ≤ Y.

```javascript
function solution(X, Y, D) {
  return Math.ceil((Y - X) / D);
}
```

### [PermMissingElem](https://app.codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/)

An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

```
function solution(A);
```

that, given an array A, returns the value of the missing element.

For example, given array A such that:

```
A[0] = 2
A[1] = 3
A[2] = 1
A[3] = 5
```

the function should return 4, as it is the missing element.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [0..100,000];
- the elements of A are all distinct;
- each element of array A is an integer within the range [1..(N + 1)].

#### 나의 풀이

**스코어 50%, 시간 초과**

```javascript
function solution(A) {
  let result = 1;
  const sortedArray = A.sort();

  for (let i = 0; i < A.length; i++) {
    if (result !== sortedArray[i]) {
      break;
    }

    result++;
  }

  return result;
}
```

위의 풀이의 경우 시간 복잡도가 O(N+logN)일 것으로 추정된다. 한참 고민해도 모르겠어서 인터넷에서 찾아보니 수열의 합 공식을 이용해서 푸는 방법이 있었다. 이렇게 푸는 경우 시간 복잡도가 O(N) 이하로 떨어진다.

**스코어 100%**

```javascript
function solution(A) {
  const n = A.length;
  let result = ((n + 1) * (n + 2)) / 2;

  for (let i = 0; i < n; i++) {
    result -= A[i];
  }

  return result;
}
```

## Lesseon 4 Counting Elements

### FrogRiverOne

A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given an array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, we want to find the earliest moment when all the positions from 1 to X are covered by leaves). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:

```
A[0] = 1
A[1] = 3
A[2] = 1
A[3] = 4
A[4] = 2
A[5] = 3
A[6] = 5
A[7] = 4
```

In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:

```
class Solution { public int solution(int X, int[] A); }
```

that, given a non-empty array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

For example, given X = 5 and array A such that:

```
A[0] = 1
A[1] = 3
A[2] = 1
A[3] = 4
A[4] = 2
A[5] = 3
A[6] = 5
A[7] = 4
```

the function should return 6, as explained above.

Write an efficient algorithm for the following assumptions:

- N and X are integers within the range [1..100,000];
- each element of array A is an integer within the range [1..X].

#### 나의 풀이

**스코어 81%**

```javascript
function solution(X, A) {
  const array = new Array(X);

  for (let i = 0; i < A.length; i++) {
    const position = A[i];
    array[position - 1] = true;

    let hasEmpty = false;
    for (let j = 0; j < array.length; j++) {
      if (array[j] === undefined) {
        hasEmpty = true;
        break;
      }
    }

    if (!hasEmpty) {
      return i;
    }
  }

  return -1;
}
```

위처럼 푸는 경우 시간 복잡도가 최대 O(N^2)가 되어 성능 점수가 떨어진다. for문 안에서 for문을 돌지 않게 하는 방법을 다시 고민해보았다. 중복을 자동으로 제거해주는 set을 이용하면 for문 한 번으로 가능! 그러면 시간 복잡도가 O(N)으로 줄어든다.

```javascript
function solution(X, A) {
  const array = new Array(X);
  const positionSet = new Set();

  for (let i = 0; i < A.length; i++) {
    const position = A[i];
    positionSet.add(position);

    if (positionSet.size === X) {
      return i;
    }
  }

  return -1;
}
```

## Lesson 6 Sorting

### [Distinct](https://app.codility.com/programmers/lessons/6-sorting/distinct/)

Write a function

```
function solution(A);
```

that, given an array A consisting of N integers, returns the number of distinct values in array A.

For example, given array A consisting of six elements such that:

```
A[0] = 2    A[1] = 1    A[2] = 1
A[3] = 2    A[4] = 3    A[5] = 1
```

the function should return 3, because there are 3 distinct values appearing in array A, namely 1, 2 and 3.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [0..100,000];
- each element of array A is an integer within the range [−1,000,000..1,000,000].

#### 나의 풀이

```javascript
function solution(A) {
  const numberSet = new Set();

  for (let i = 0; i < A.length; i++) {
    numberSet.add(A[i]);
  }

  return numberSet.size;
}
```

위와 같이 풀었으나... 해당 레슨이 sort인데 이렇게 풀어버려서 찜찜.. 흠..
