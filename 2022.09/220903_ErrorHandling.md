# ✏️ TIL (Today I Learned)

# Error Handling

- 에러처리는 프로그램의 에러 조건에서 응답하고 복구하는 프로세스
- Swift는 런타임에 복구 가능한 에러를 던지고 포착하고 전파하고 조작하기 위한 최고 수준의 지원을 한다.
- 일부 작업은 항상 실행을 완료하거나 유용한 출력을 생성한다고 보장하지 않는다.
- 옵셔널은 값이 없음을 나타내는데 사용되지만 작업이 실패할 경우 코드가 그에 따라 응답할 수 있도록 에러의 원인을 이해하는 것이 유용한 경우가 많다.

> NOTE
> 
> 
> Swift에서 에러 처리는 Cocoa와 Objective-C에 NSError를 사용하는 에러 처리 패턴과 상호 운용된다.
> 

## Representing and Throwing Errors

Swift에서 에러는 Error 프로토콜에 준수하는 타입의 값으로 표현된다.

Swift 열거형은 관련된 에러 조건의 그룹을 모델링하는데 특히 적합하며 관련값을 사용하여 에러의 특성에 대한 추가 정보를 전달할 수 있다.

다음은 게임 내에서 쥬스 판매기를 작동하는 에러 조건을 나타내는 방법이다.

```swift
enum JuiceMakerError: Error {
    case invalidSelection
    case outOfStock
    case insufficientFunds(coinsNeeded: Int)
}
```

에러가 발생하면 예상치 못한 일이 발생하여 정상적인 흐름을 계속할 수 없음을 나타낼 수 있다.

throw 구문을 사용하여 에러를 발생 시킵니다.

```swift
throw JuiceMakerError.insufficientFunds(coinsNeeded: 1000)
```

## Handling Errors

에러가 발생할 때 주변 코드의 부분이 에러 처리를 담당해야 한다. 예를 들어 문제를 수정하거나 다른 방법을 시도하거나 사용자에게 에러를 알리는 방법으로 에러 처리를 해야한다.

Swift에서는 에러를 처리하는 4가지 방법이 있다. 함수에서 해당 함수를 호출하는 코드로 에러를 전파 하거나 do - catch 구문을 사용하거나 옵셔널 값으로 에러를 처리하거나 에러가 발생하지 않을 것이라고 주장할 수 있다.

함수에서 에러가 발생하면 프로그램의 흐름이 변경되므로 코드에서 에러가 발생할 수 있는 위치를 신속하게 알 수 있어야 한다. 코드에서 이러한 위치를 식별하려면 에러가 발생할 수 있는 함수, 메서드, 또는 초기화 구문 호출하는 코드 이전에 try 또는 try? 또는 try! 키워드를 작성해야 한다.

## throw 함수를 이용한 에러 전파

에러가 발생할 수 있는 함수, 메서드, 또는 초기화 구문을 나타내기 위해 파라키너 뒤에 함수의 선언에 throw키워드를 작성해 줍니다!

```swift
func makeJuice(juiceNamed name: String) throws
```

throw함수는 내부에서 발생한 에러를 호출된 범위로 전파합니다.

> NOTE
> 
> 
> throw 함수는 에러만 전파 할 수 있습니다. throw선언이 되지 않은 함수 내에서 발생된 모든 에러는 함수 내에서 처리해야한다.
> 

```swift
struct Juice {
    var amount: Int
    var price: Int
}

class JuiceMaker {
    var inventory = [
        "Strawberry Juice": Juice(amount: 500, price: 4500),
        "Kiwiw Juice": Juice(amount: 300, price: 5000),
        "Watermelon Juice": Juice(amount: 1000, price: 3000)
    ]
    var coinsDeposited = 0
    
    func makeJuice(juiceNamed name: String) throws {
        guard let juice = inventory[name] else {
            throw JuiceMakerError.invalidSelection
        }
        
        guard juice.amount > 0 else {
            throw JuiceMakerError.outOfStock
        }
        
        guard juice.price <= coinsDeposited else {
            throw JuiceMakerError.insufficientFunds(coinsNeeded: juice.price - coinsDeposited)
        }
        
        coinsDeposited -= juice.price
        
        print("\(name) 나왔습니다~")
    }
}
```

예제를 보자.

`makeJuice(juiceNamed:)` 메서드의 구현은 `guard` 구문을 사용하여 메서드를 일찍 종료시키고 wbtm 구매 요구사항 중 하나라도 충족하지 않으면 적절한 에러를 발생합니다. `throw`구문은 프로그램 제어를 즉시 전달하므로 항목은 요구사항이 모두 만족해야만 판매됩니다.
