# [Close 함수](#close)

* Go 버전: 1.9
* 원문: [Close](https://golang.org/ref/spec#Close)
* 번역자: Joseph Kim (@superbmilkyway)

채널 c에 대해 내장 함수 `close(c)`는 더는 값을 채널 c에 보내지 않을 것을 선언한다. 만약 채널 c가 받기 전용 채널이라면 이는 오류를 발생시킨다. 닫힌 채널에 값을 전송하거나 다시 닫으려고 하면 [런타임 패닉](/Run-time panics/)을 일으킨다. nil 채널을 닫는 것도 [런타임 패닉](/Run-time panics/)을 일으킨다. close 호출 후에 그리고 이전에 보내진 모든 값을 받은 이후의 받기(receive) 작업은 블로킹 없이 채널 타입을 위해 0 값을 반환할 것이다. 다중 값 [받기 작업](/Expressions/receive_operator.html)은 채널의 닫힘 여부를 알려주는 신호와 함께 받은 값을 반환한다.
