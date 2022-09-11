# ✏️ TIL (Today I Learned)

# 🔥 공부한 내용

## Protocol

프로토콜은 메서드, 프로퍼티, 그리고 특정 작업이나 기능의 부분이 적합한 다른 요구사항의 청사진을 정의합니다.

프로토콜은 요구사항의 구현을 제공하기 위해 클래스, 객체, 또는 열거형에 의해 채택될 수 있다.

포토코롱의 요구사항에 충족하는 모든 타입은 프로토콜에 **준수**한다고 한다.

준수하는 타입의 요구사항을 지정하는 것 외에도 요구 사항의 일부를 구현하거나 준수하는 타입에 추가기능을 구현하기 위해 프로토콜을 확장(Extension)할 수 있습니다.

---

## 프로토콜 구문 정의

클래스, 구조체, 그리고 열거형과 유사한 방법으로 정의합니다.

```swift
protocol SomeProtocol {
		// 프로토콜 정의는 여기에!
}
```

사용자 정의 타입은 콜론으로 구분된 타입의 이름 뒤에 특정 프로토콜의 이름을 적어 특정 프로토콜을 채택합니다.

여러 프로토콜은 콤마로 구분되고 목록화 할 수 있다.

```swift
struct SomeStructure: FirstProtocol, SecondProtocol {
		// sturct 정의는 여기에!
}
```

클래스가 상위 클래스를 가진 경우에는 콤마로 구분해서, 채택할 프로토콜 앞에 적는다.

```swift
class SomeClass: SomeSuperClass, FirstProtocol, SecondProtocol {
		// class 정의는 여기에!
}
```

---

## 프로퍼티 요구사항

프로퍼티는 특정 이름과 타입을 가진 인스턴스 프로퍼티 또는 타입 프로퍼티를 제공하기 위해 모든 준수하는 타입을 요구합니다. 프로토콜은 요구된 프로퍼티 이름과 타입만 지정하고 프로퍼티가 저장 또는 계산 프로퍼티인지에 대한 것은 지정하지 않습니다. 프로토콜은 각 프로퍼티가 gettable, settable에 대한 정보도 지정해줘야 합니다.

프로토콜이 gettable과 settable 인 프로퍼티를 요구할 경우 프로퍼티 요구사항은 저장된 프로퍼티 상수 또는 읽기전용 계산된 프로퍼티는 충족할 수 없습니다. 프로토콜이 gettable 인 프로퍼티 만 요구할 경우 이 요구사항은 모든 종류의 프로퍼티에 충족될 수 있고 이것이 유용한 경우 settable 또한 프로퍼티에 대해 유효합니다.

프로퍼티 요구사항은 항상 `var`키워드와 함께 변수 프로퍼티로 선언됩니다. gettable과 settable 프로퍼티는 타입 선언 뒤에 `{ get set }`으로 작성하여 나타내고 gettable 프로퍼티는 `{ get }`으로 작성하여 나타냅니다.

```swift
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}
```

항상 프로토콜에서 정의할 때 static 키워드 타입 프로퍼티 요구사항에 접두사로 둡니다. 이 규칙은 타입 프로퍼티 요구사항은 클래스에 의해 구현 될 때 class 또는 static 키워드를 붙일 수 있는 경우에도 적용되빈다.

```swift
protocol AnotherProtocol {
    static var someTypeProperty: Int { get set }
}
```

다음은 단일 인스턴스 프로퍼티 요구사항을 가지는 프로토콜 예시입니다.

```swift
protocol FullyNamed {
    var fullName: String { get }
}
```

`fullyNamed`프로토콜은 완벽한 이름을 제공하기 위해 준수하는 타입을 요구합니다. 이 프로토콜은 다른 준수하는 타입을 지정하지 않으며 타입이 자체에 대한 전체 이름을 제공해야 된다고만 지정합니다. 이 프로토콜은 모든 `FullyNamed` 타입이 `String` 타입의 `fullName` 이라는 gettable 인스턴스 프로퍼티를 가져야 합니다.

그럼 `fullyNamed`프로토콜을 채택하고 준수하는 구조체는?

```swift
struct Person: FullyNamed {
    var fullName: String
}
let john = Person(fullName: "John Appleseed")
// john.fullName is "John Appleseed"
```

 

이 예제는 특정 이름을 가진 사람을 나타내는 Person 이라는 구조체를 정의합니다. 첫 번째 줄을 보면 `fullyNamed`프로토콜도 채택하고 있습니다.

Person의 각 인스턴스는 String 타입의 fullName 이라는 단일 저장된 프로퍼티를 가집니다. 이것은 `fullyNamed`프로토콜의 단일 요구사항과 일치하고 Person은 프로토콜을 올바르게 준수하고 있다고 얘기합니다.

---

## 메서드 요구사항 변경

메서드가 속한 인스턴스를 수정 또는 변경해야하는 경우가 있습니다. 값 타입에 대한 인스턴스 메서드의 경우 메서드의 func 키워드 앞에 mutating 키워드를 위치시켜 메서드가 속한 인스턴스와 인스턴스의 모든 프로퍼티를 수정할 수 있음을 나타낸다. 

프로토콜을 채택하는 모든 타입의 인스턴스를 변경하기 위한 포로토콜 인스턴스 메서드 요구사항을 정의하는 경우 프로토콜의 정의의 부분으로 mutating 키워드로 메서드를 표시한다. 이를 통해 구조체와 열거형이 프로토콜을 채택하고 메서드 요구사항을 충족할 수 있습니다.

<aside>
✏️ mutating 으로 프로토콜 ㅇ니스턴스 메서드 요구사항을 표시하면 클래스에 대한 해당 메서드의 구현을 작성할 때 mutating 키워드로 메서드를 표시합니다. 이를 통해 구조체와 열거형이 프로토콜을 채택하고 메서드 요구사항을 충족할 수 있습니다.

</aside>

다음은 protocol을 활용한 예제

```swift
protocol Togglable {
    mutating func toggle()
}

enum OnOffSwitch: Togglable {
    case off, on
    mutating func toggle() {
        switch self {
        case .off:
            self = .on
        case .on:
            self = .off
        }
    }
}
var lightSwitch = OnOffSwitch.off
lightSwitch.toggle()
// lightSwitch is now equal to .on
```

`toggle()` 에 대한 정의는 protocol에서 하지 않고 porotocl을 채택하는 구조체, 클래스, 열거형에서 정의힌다.

---

## 초기화 구문 요구사항

프로토콜은 준수하는 타입에 의해 지정된 초기화 구문을 요구할 수 있습니다. 일반적인 초기화 구문과 동일한 방식으로 프로토콜의 정의 부분과 초기화 구문을 작성하지만 중괄호 또는 초기화 구문 바디 없이 작성합니다.

```swift
protocol SomeProtocol {
    init(someParameter: Int)
}
```

### 프로토콜 초기화 구문 요구사항의 클래스 구현

지정된 초기화 구문 또는 편의 초기화 구문으로 준수하는 클래스에 프로토콜 초기화 구문 요구사항을 구현할 수 있습니다. 이 모든 케이스에 대해 required 수식어와 함께 초기화 구문 구현에 표시해야 한다.

```swift
class SomeClass: SomeProtocol {
    required init(someParameter: Int) {
        // initializer 
    }
}
```

required 수식어를 사용하면 준수하는 클래스의 모든 하위 클래스에 초기화 구문 요구사항의 명시적 또는 상속된 구현을 제공하여 Protocol을 준수할수 있다.

<aside>
✏️ final 클래스는 하위 클래스를 생석할 수 없으므로 final 수식어로 표시된 클래스에 required 수식어 프로토콜 초기화 구문 구현에 표시할 수 없다.

</aside>

---

## 타입으로 프로토콜

프로토콜 자체는 어떤 기능도 구현하지 않는다. 그럼에도 불구하고 프로토콜을 코드에서 완전한 타입으로 사용할 수 있다. 타입으로 프로토콜을 사용하는 것은 “T가 프로토콜을 준수하는 타입 T가 존재한다" 라는 구절에서 비롣된 것이다.

다음을 포함해 다른 타입이 허용되는 여러 위치에서 프로토콜을 사용할 수 있다.

- 함수, 메서드, 또는 초기화 구문에서 파라미터 타입 또는 반환타입으로
- 상수, 변수, 또는 프로퍼티 타입으로
- 배열, 딕셔너리, 또는 다른 컨테이너에서 항목의 타입

<aside>
✏️ 프로토콜은 타입이므로 프로토콜의 이름은 대문자로 시작합니다!

</aside>

---

## Delegation

위임은 클래스 또는 구조체가 책임의 일부를 다른 타입의 인스턴스에 넘겨주거나 위임할 수 있도록 하는 디자인 패턴이다. 이 디자인 패턴은 위임된 기능을 제공하기 위해 준수하는 타입이 보장되도록 위임된 책임을 캡슐화하는 프로토콜을 정의하여 구현한다. 위임은 특정 작업에 응답하거나 해당 소스의 기본 타입을 알 필요 없이 외부 소스에서 데이터를 검색하는데 사용할 수 있다.

```swift
protocol DiceGame {
    var dice: Dice { get }
    func play()
}
protocol DiceGameDelegate: AnyObject {
    func gameDidStart(_ game: DiceGame)
    func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)
    func gameDidEnd(_ game: DiceGame)
}
```

```swift
class SnakesAndLadders: DiceGame {
    let finalSquare = 25
    let dice = Dice(sides: 6, generator: LinearCongruentialGenerator())
    var square = 0
    var board: [Int]
    init() {
        board = Array(repeating: 0, count: finalSquare + 1)
        board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
        board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
    }
    weak var delegate: DiceGameDelegate?
    func play() {
        square = 0
        delegate?.gameDidStart(self)
        gameLoop: while square != finalSquare {
            let diceRoll = dice.roll()
            delegate?.game(self, didStartNewTurnWithDiceRoll: diceRoll)
            switch square + diceRoll {
            case finalSquare:
                break gameLoop
            case let newSquare where newSquare > finalSquare:
                continue gameLoop
            default:
                square += diceRoll
                square += board[square]
            }
        }
        delegate?.gameDidEnd(self)
    }
}
```

DiceGameDelegate 프로토콜은 DiceGame의 진행사항을 추적하기위해 채택 될 수 있다.

강한 참조 사이클을 방지하기 위해 위임자는 weak로 선언 된다. 프로토콜을 클래스 전용 프로토콜로 표시하면 이 챕터의 뒷부분에서 `SnakesAndLadders`클래스는 위임자가 약한 참조로 사용되어야 한다고 선언할 수 있습니다. [클래스 전용 프로토콜 (Class-Only Protocols)](notion://www.notion.so/swift/language-guide-1/protocols#class-only-protocols)은 `AnyObject`의 상속으로 표시됩니다.

# ****🔥 오늘의 3줄 회고****

- 
- 
-