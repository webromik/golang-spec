# [길이와 용량](#length-and-capacity)

* Go 버전: 1.9
* 원문: [Length and capacity)](https://golang.org/ref/spec#Length_and_capacity)
* 번역자: Joseph Kim (@superbmilkyway)

내장 함수 len과 cap은 다양한 타입의 인자를 받고 int 타입의 결과를 반환한다. 이 두 함수의 구현은 결과가 항상 int 타입과 일치되는 것을 보장한다.

```golang
호출      인자 타입         결과

len(s)    string 타입      문자열 길이 (바이트 단위)
          [n]T, *[n]T      배열의 길이 (== n)
          []T              슬라이스의 길이
          map[K]T          맵의 길이 (정의된 키의 개수)
          chan T           채널 버퍼에 들어 있는 원소의 개수

cap(s)    [n]T, *[n]T      배열의 길이 (== n)
          []T              슬라이스 용량
          chan T           채널 버퍼 용량
```

슬라이스의 용량은 슬라이스 기저 배열에 할당된 공간에서의 원소의 개수이다. 항상 다음의 관계를 유지한다:

```golang
0 <= len(s) <= cap(s)
```

nil 슬라이스, nil 맵, nil 채널의 길이는 0 이다. nil 슬라이스 또는 nil 채널의 용량은 0 이다.

만약 s가 문자열 상수이면, 식 `len(s)`는 [상수](/Constants/)이다. 만약 s의 타입이 배열 또는 배열의 포인터이고 식 s가 [채널 수신자](/Expressions/receive_operator.html) 또는 (상수가 아닌)[함수 호출](/Expressions/calls.html)을 포함하면 `len(s)`과 `cap(s)`은 상수이다. 그리고 이 경우에는 s는 평가 되지 않는다. 이 경우를 제외하면, len과 cap의 호출은 상수가 아니며 s는 평가된다.

```golang
const (
	c1 = imag(2i)                    // imag(2i) = 2.0은 상수다
	c2 = len([10]float64{2})         // [10]float64{2}은 힘수 호출을 포함하지 않는다
	c3 = len([10]float64{c1})        // [10]float64{c1}은 힘수 호출을 포함하지 않는다
	c4 = len([10]float64{imag(2i)})  // imag(2i)은 상수이고 함수 호출이 아님
	c5 = len([10]float64{imag(z)})   // 잘못됨: imag(z)는 (상수가 아닌) 함수 호출이다
)
var z complex128
```