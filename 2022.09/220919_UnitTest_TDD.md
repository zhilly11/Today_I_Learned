# 220919_UnitTest

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  UnitTest 학습
- [ ]  계산기 프로젝트 시작
- [ ]  

# 🔥 오늘 한 일

## Unit Test 공부

## 활동 학습

### Unit Test

코드를 검증하는 코드를 만든다.

가짜 객체는 sut (system under test) 변수명으로 한다.

유닛테스트에는 3가지 순서가 있다.

given - 이런 가정에서

when - 이렇게 하면

 then - 결과가 이렇다.

테스트 메서드 네이밍은 앞에 항상 test를 붙인다.

TDD
RED를 먼저 

실패할 할 수도 있는 테스트를 방지하려고

테스트와 코드 사이에는 연관성이 없어야 한다.

"**테스트는 구현의 보조적인 수단인데**, 이를 위해 구현부 설계가 교체되는게 옳은것인가"

→ 

"**테스트를 위해 구현 설계가 변경될 수 있다**.테스트 코드는 구현의 보조적인 수단이 아니며, 같은 레벨로 봐야한다.**좋은 디자인으로 구현된 코드는 대부분 테스트 하기가 쉽다**.테스트 하기 어렵게 구현 되었다면, 코드 확장성 / 의존성 등 코드 디자인, 설계가 잘못되었을 확률이 굉장히 높다."

**테스트하기 좋은 코드 vs 테스트하기 어려운 코드?**

→

경험상 **몇번을 수행해도 항상 같은 결과**가 반환되는 함수 (`멱등성이 보장되는 순수함수`) 가 테스트하기 좋은 코드였다.

몇번을 수행해도 항상 같은 결과가 나오기 위해서는 아래 2가지 요소를 최대한 피해해야만 한다.

1. **제어할 수 없는 값에 의존하는 경우 (ex) random(), readLine(), 전역함수, 전역변수)**
2. 외부에 영향을 주는 코드(ex) print(), debugPrint(), database등에 의존하는 경우)

# ****🔥 공부한 내용****

## 의존성 주입

의존성 주입은 하나의 객체가 다른 객체의 의존성을 제공하는 기술

## 먼저 의존성이란?

```swift
class Car {
        // 어떤 객체가 내부에서 생성하여 가지고 있는 객체를 의존성이라고 한다.
        // 여기서는 wheel이 의존성
    var wheel: Wheel = Wheel()
}

class Wheel {
    var weight = 10
}
```

위의 코드에서는 Car가 wheel에 대한 의존성을 가지고 있기 때문에 Car가 Wheel에게 의존하고 있다 라고 말할 수 있다.

## 의존성 주입이란?

```swift
class Car {
    var wheel: Wheel

    init(wheel: Wheel) {
        self.wheel = wheel
    }
}

class Wheel {
    var weight = 10
}

let myWheel = Wheel()
let myCar = Car(wheel: myWheel)
```

의존성 주입이란 말 그대로 의존성을 *주입* 시킨다는 뜻입니다. 내부에서 초기화가 이루어지는 것이 아니라 외부에서 객체를 생성하여 내부에 **주입**해주는 것입니다. 위 코드에서는 myWheel을 외부에서 생성하여 Car를 초기화할 때 myWheel을 **주입**시켜주고 있습니다.

## 그럼 의존성 주입은 왜 쓸까?

객체간 결합도를 낮추기 위해 사용한다. 객체간 결합도가 낮으면 리팽토링이 쉽고, 테스트 코드 작성이 쉬워진다는 장점이 있다.

```swift
class UpDownGame {
    var randomValue: Int = 0
    var tryCount: Int = 0
    var urlSession: URLSessionProtocol

    init(urlSession: URLSessionProtocol = URLSession.shared) {
        self.urlSession = urlSession
    }

    ...
}
```

예제 코드에서는 `URLSessionProtocol`이라는 프로토콜을 만들어서 직접적으로 URLSession을 타입으로 만들지 않고 의존성을 주입할 수 있도록 되어있습니다. 이렇게 의존성을 주입하도록 만든 이유는 테스트를 진행할 때에는 앞서 설명했던 Test Double 객체를 실제 URLSession의 자리에 바꿔치기 시키면서 테스트를 진행시키기 위함입니다. 이는 결합도가 낮아졌기 때문에 가능한 이야기라고 할 수 있습니다.

[야곰닷넷 UnitTest](https://www.notion.so/UnitTest-94b2abd524c6401981135da8bce7f00b)

# ****🔥 오늘의 3줄 회고****

- 개인 프로젝트할때는 시간을 잘 쪼개서 쓰자,, 하루가 어떻게 가는지 모르겠다.
- 학습활동 예습을 완벽하게 하고 가지 않으면 못따라 갈듯,,
- 계산기프로젝트도 열심히 해보자🔥
