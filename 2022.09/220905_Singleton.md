# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [x]  singleton 패턴 공부
- [x]  쥬스메이커 STEP-2 사전학습

# 🔥 오늘 한 일

## Singleton

싱글톤 클래스는 응용 프로그램이 요구하는 횟수에 관계없이 동일한 인스턴스를 반환한다.

표준 클래스에서는 발신자가 원하는 수만큼 클래스의 인스턴스를 만들 수 있지만 싱글톤 클래스의 경우 프로세스별로 클래스의 인스턴스를 1개만 만들 수 있다.

싱글톤 오브젝트는 클래스의 자원에 대한 글로벌 엑세스 포인트를 제공한다.

싱글톤은 일반적인 서비스나 리소스를 제공하는 클래스 등 단일 제어 포인트가 필요한 상황에서 사용된다.

<aside>
🤔 여기까지 보면 싱글톤클래스는 클래스에 대한 인스턴스 생성을 한 개로 제한하면서 엑세스 포인트를 제공하고 단일제어를 조금 더 효율적?으로 할 수 있기 위해 사용하는 것 같다.

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72dc24a9-91bd-463c-85a6-6cdad4232dc2/Untitled.png)

글로벌 인스턴스는 싱글톤 클래스에서 팩토리 메서드를 사용해 가져온다.

클래스는 처음 요청할 때 해당 인스턴스를 lazy 만든 후 다른 인스턴스를 만들 수 없도록 한다.

싱글톤 클래스에서는 발신자가 인스턴스를 복사, 유지 또는 해제할 수도 없다.

필요에 따라, 독자적인 싱글톤 클래스를 작성할 수 있다.

몇몇 코코아 프레임워크 클래스는 싱글통이다.

ex) `UIKit` 에서 `UIApplication`, `UIAccelremotersingleton instance`

## 🤔 그럼 Singlton Class는 어떻게 정의하고 어떻게 접근할까?

### 정의

```swift
final class FruitStock {
    static let shared = FruitStock()
    
    var appleAmount: Int?
    var bananaAmount: Int?
    
    private init() {
        
    }
}

final class FuitStore {
	static let shared = FuritStore()
	
	private var fruitStock: [Fruit: Int] = [
        .strawberry: 10,
        .banana: 10,
        .kiwi: 10,
        .pineapple: 10,
        .mango:10
  ]

	private init() {
	}
	
	func ... () 
	.
	.
	.
}
```

1. 먼저 `final` 을 사용하여 `class`의 이름을 작성해준다.
2. 전역으로 저장될거니까, `static`을 이용해 `Instance`를 저장할 프로퍼티 생성
3. `init` 함수를 `private`로 지정해 `init` 함수를 호출해 다른 `Instance`를 생성해주는 것을 막는다.

✏️ 이런식으로 클로져를 이용하여 사용할 수도 있다!

```swift
final class FruitStock {
    static let shared: FruitStock = {
        let instnace = FruitStock()
        print("Fruit Stock hello")
        return instnace
				// setup code
    }()
    
    var appleAmount: Int?
    var bananaAmount: Int?
    
    private init() {
        
    }
}
```

### 접근

```swift
let fruitStockInfo = FruitStock.shared
```

어디서든 shared라는 전역변수를 사용하면 하나의 인스턴스를 공유해 사용할 수 있다.

## 싱글톤의 장점?

- 한 번의 Instance만 생성하니까 메모리 낭비 방지!
- 다른 클래스들과 자원 공유가 쉬움!
- 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용한다!

## 싱글톤의 단점?

- init 을 private으로 제한해버리기 때문에 테스트가 어렵다.
- Singleton Instance가 너무 많은 일을 하거나, 많은 데이터를 공유시킬경우에 다른 클래스의 Instance들 간의 결합도가 높아져 “개방 폐쇄”원칙을 위배하게 된다.
- 따라서 수정과 테스트가 어려워 진다.

### 참고

[https://babbab2.tistory.com/66](https://babbab2.tistory.com/66)

# ****🔥 오늘의 3줄 회고****

- 배움엔 끝이없다
- 머리속으로 생각 정리가 안될때는 항상 적자 적자 적자
- 시간을 쪼개서 쓰자 no time no time no time