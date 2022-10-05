# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [x]  Nested Types 정리
- [ ]  Error Handling, Result type 공부


# 🔥 오늘 한 일

### 쥬스메이커 STEP-1 최종 리팩터링

### README Day!

# ****🔥 공부한 내용****

## Nested Types

열거형은 특정 클래스 또는 구조체의 기능을 지원하기 위해 사용한다!

더 복잡한 타입의 컨텍스트 내에서 사용하기 위해 순수하게 유틸리티 클래스와 구조체를 정의하는것이 편리할 수 있다.

이를 위해 Swift는 Nested Types 를 정의 할 수 있으며 타입의 정의 내에서 지원하는 열거현, 클래스, 구조체를 중첩할 수 있다.

다른 타입 내에서 중첩하려면 지원하는 타입의 외부 중괄호 내에 정의를 작성해야 한다.

## Nested Types의 동작

아래 예제는 쥬스 종류에 따라 쥬스 레시피를 가지고 있는 JuiceMaker 라는 클래스 입니다.

JuiceMaker 클래스는 Fruit와 Juice라는 중첩된 열거형 그리고 displayRecipe함수를 가지고 있습니다!

```swift
class JuiceMaker {
    enum Fruit {
        case strawberry
        case banana
    }
    
    enum Juice {
        case strawberryJuice
        case bananaJuice
        case strawberryBananaJuice
        
        struct Recipe {
            let fruit: Fruit
            let amount: Int
        }
        
        var recipe: [Recipe] {
            switch self {
            case .strawberryJuice:
                return [Recipe(fruit: .strawberry, amount: 16)]
            case .bananaJuice:
                return [Recipe(fruit: .banana, amount: 2)]
            case .strawberryBananaJuice:
                return [Recipe(fruit: .strawberry, amount: 10), Recipe(fruit: .banana, amount: 1)]
            }
        }
    }
    
    func displayRecipe(selectJuice: Juice){
        for juice in selectJuice.recipe {
            print("\(juice.fruit): \(juice.amount)개 필요")
        }
    }
}

```

차근차근 하나식 보실까요?

```swift
class JuiceMaker {
    enum Fruit {
        case strawberry
        case banana
    }
...
```

먼저 JuiceMaker 라는 클래스를 하나 만들어 줬습니다. 그리고 안에 Fruit 라는 enum을 하나 생성해 주었습니다.

> Swift는 *중첩된 타입 (nested types)*을 정의할 수 있으며 지원하는 타입의 정의 내에서 지원하는 열거형, 클래스, 그리고 구조체를 중첩할 수 있습니다. 타입은 필요한만큼의 수준으로 중첩될 수 있습니다.
> 

라는 문구를 통해 우리는 지원하는 타입안에서는 필요한 수준만큼! 열거형, 클래스, 구조체를 중첩할 수 있다는 것을 알 수 있습니다.

```swift
enum Juice {
        case strawberryJuice
        case bananaJuice
        case strawberryBananaJuice
        
        struct Recipe {
            let fruit: Fruit
            let amount: Int
        }
        
        var recipe: [Recipe] {
            switch self {
            case .strawberryJuice:
                return [Recipe(fruit: .strawberry, amount: 16)]
            case .bananaJuice:
                return [Recipe(fruit: .banana, amount: 2)]
            case .strawberryBananaJuice:
                return [Recipe(fruit: .strawberry, amount: 10), Recipe(fruit: .banana, amount: 1)]
            }
        }
    }
```

그 밑에 또다른 enum인 Juice를 작성해주었습니다! 

Juice 안에는 case로 주스 이름들이 정의되어 있고 enum안에 Recipe라는 구조체도 또 정의해주었네요

```swift
func displayRecipe(selectJuice: Juice){
        for juice in selectJuice.recipe {
            print("\(juice.fruit): \(juice.amount)개 필요")
        }
}
```

JuiceMaker안에 메서드도 구현되어 있습니다! 

구조를 보게 되면

```swift
class JuiceMaker
├── enum Fruit
├── enum Juice
│   ├── struct Recipe
│   └── var recipe: [Recipe]
└── func displayRecipe(Juice)
```

이런 식으로 class 안에 enum 안에 struct, var 이 정의 되어 있습니다!

여기까지가 Nested Type 예제 Class 였습니다.

그렇다면 Juice 클래스의 인스턴스는 어떻게 생성할까요?

```swift
var juiceMaker = JuiceMaker()
juiceMaker.displayRecipe(selectJuice: JuiceMaker.Juice.strawberryBananaJuice)
```

JuiceMaker는 클래스라 암시적 이니셜라이즈가 존재합니다!

매개변수 부분을 보시면 JuiceMaker의 enum Juice의 .strawwberryBananaJuice 까지 호출이 잘 되는군요!

```swift
// func displayRecipe 결과
strawberry: 10개 필요
banana: 1개 필요
Program ended with exit code: 0
```

## 참고

[Swift Language - Nested Types](https://docs.swift.org/swift-book/LanguageGuide/NestedTypes.html)

[https://zeddios.tistory.com/322](https://zeddios.tistory.com/322)

끝!

# ****🔥 오늘의 3줄 회고****

- 예제를 만들어 보자. 항상
- 코드에 정답은 없다. 진짜
- 기록을 습관화 하자. 제발

