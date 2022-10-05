# 220927_CharacterSet,Closure

Date: 2022년 9월 27일

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [x]  STEP-2 PR 보내기
- [x]  오토레이아웃 2 듣기 (활동학습 예습)
- [x]  고차함수 공부
- [x]  Protocol 마저 읽기

# 🔥 오늘 한 일

## 계산기 STEP-2 PR 보냄!

## Closure 강의 들음!

## AutoLayout 강의 들음!

## Protocol 문서 추가로 읽음!

# ****🔥 공부한 내용****

## Closure

클로저는 일급 객체다. 따라서 전달인자, 변수, 상수 등으로 저장, 전달 가능

```swift
let sum: (Int, Int) -> Int = { (a: Int, b: Int) in
    return a + b
}
var result = sum(1,2)

func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
    return method(a, b)
}

//후행 클로저
// 클로저가 함수의 마지막 전달인자라면
// 마지막 매개변수 이름을 생략한 후
// 함수 소괄호 외부에 클로저를 구현할 수 있다.
result = calculate(a: 10, b: 10) { (left: Int, right: Int) -> Int in
    return left + right
}
// 마지막 인자로 전달될 친구가 클로져구나

//반환타입 생략
// calculate함수의 method 매개변수는
// Int타입을 반환할 것이라는 사실을 컴파일러도 알기 때문에
// 굳이 클로저에서 반환타입을 명시해 주지 않아도 된다.
// 대신 in 키워드는 생략할 수 없다.
result = calculate(a: 10, b: 10, method: { (left: Int, right: Int) in
    return left + right
})

//후행 클로저와도 같이 사용 가능
result = calculate(a: 10, b: 10) { (left: Int, right: Int) in
    return left + right
}

//단축 인자이름
result = calculate(a: 10, b: 10, method: {
    return $0 + $1
})

// 당연히 후행 클로저와 같이 사용 가능
result = calculate(a: 10, b: 10) {
    return $0 + $1
}

//암시적 반환 표현
// 클로저가 반환하는 값이 있다면 클로저의 마지막 줄의 결과값은 암시적으로 반환값으로 취급합니다.
result = calculate(a: 10, b: 10) {
    $0 + $1
}
```

`in` 은 매개변수와 실행코드를 구분짓기 위해 사용한다.

## AutoLayout

제약조건이 겹칠때 → priority 설정. 우선순위 높을 수록 높은 값!

비율로 설정하는 법 → multiple 값으로 설정

높이 너비 같게 하는법 → 컨트롤누르고 자신한테 드래그 → 옵션키 누르면 1대1설정 나옴!

### CharacterSet

왜 CharacterSet을 공부하게 되었냐면 ****[`components(separatedBy:)`](https://beepeach.tistory.com/194#components-separatedBy%-A-) 요녀석이 인자로 CharacterSet만 받아서,,, 이제는 스위프트한테 안진다는 마인드 줄여서 안진마**

정리를 해보려 했으나 여기 너무 잘 나와있어서 첨부합니다.. ^^;;

[https://beepeach.tistory.com/194](https://beepeach.tistory.com/194)

# ****🔥 문제점 → 해결 방법****

## components 사용시 CharacterSet만 사용 가능 함 ㅠ

CharacterSet이 뭔지 처음 부터 공부함

야무지게 쓸 수 있는 방법 찾음

```swift
private static func componentsByOperators(from input: String) -> [String] {
        let operators = String(Operator.allCases.map{ $0.rawValue })
        let operatorsCharacterSet:CharacterSet = CharacterSet(charactersIn: operators)

        return input.components(separatedBy: operatorsCharacterSet)
    }
```

`CharacterSet(charactersIn: String)` 이렇게 쓰면 야물딱지게 CharacterSet 만들어줌!

# ****🔥 오늘의 3줄 회고****

- 진짜 이번 주말로 더 안미룰 예정
- 못한건 안자고 할 예정
- 곧 기절할 예정