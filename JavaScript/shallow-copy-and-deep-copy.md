# 얕은 복사와 깊은 복사

문자열, 숫자, 불리언을 제외한 객체는 다른 변수에 대입할 때 값을 복사하는 게 아니라 참조(메모리의 주소)를 복사한다.

- shallow copy: 가장 상위 객체만 새로 생성되고 내부 객체들은 참조 관계인 경우를 의미한다.
- deep copy: 내부 객체까지 모두 새로 생성한다.

## Reference

- [객체의 복사](https://www.zerocho.com/category/JavaScript/post/5750d384b73ae5152792188d) by 제로초