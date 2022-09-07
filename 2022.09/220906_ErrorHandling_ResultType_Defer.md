# 220906_ErrorHandling_ResultType_Defer

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [x] 쥬스메이커 STEP-2 PR
- [x] 머쓱 타드 준비
- [ ] 


# ****🔥 공부한 내용****

## Error Handling

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

`makeJuice(juiceNamed:` 메서드는 발생하는 에러를 전파하기 때문에 이 메서드를 호출하는 코드는 do-catch 구문, try를 사용하여 에러를 처리하거나 계속 전파해야한다!

```swift
func sendToErrorJuice() throws {
			try JuiceMaker.makeJuice("kiwiJuice")
}
```

이런식으로 throws 를 받아 다시 한 번더 throws 시킬 수 있다!

## Do - Catch 사용하여 에러 처리하기

do - catch 구문을 사용하여 코드의 블럭을 실행하여 에러를 처리한다!

에러가 do 절에서 발생되면 catch 절과 비교하여 에러를 처리할 수 있는 항목을 결정한다.

```swift
do {
		try ((throws 구문))
		((code))
} catch ((error.name1)) {
		((code))
} catch ((error.name2)) where ((조건문)) {
		((code))
} catch ((error.name3)), ((error.name4)) {
		((code))
} catch {
		((code))
}
```

처리할 수 있는 에러가 무엇인지 나타내기 위해 catch 뒤에 패턴을 작성합니다.

catch 절이 패턴을 가지고 있지 않다면 이 절은 모든 에러와 일치하고 error 라는 이름을 가진 지역 상수로 에러를 바인드 합니다.

```swift
var juicemaker = JuiceMaker()
juicemaker.coinsDeposited = 2000

do {
    try juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
    print("쥬스 만들기 성공! 야미~")
} catch JuiceMakerError.invalidSelection {
    print("잘못된 선택 에러!")
} catch JuiceMakerError.outOfStock {
    print("재고 없음 에러!")
} catch JuiceMakerError.insufficientFunds(let coinNeeded) {
    print("금액 부족 에러! \(coinNeeded) 필요!")
} catch {
    print("알 수 없는 에러!")
}

// Prints "금액 부족 에러! 1000 필요!"
```

위의 예제에서 `makeJuice(juiceNamed:)` 는 error를 발생할 수 있으므로 try 표현식으로 호출 된다.

에러가 발생하면 실행이 즉시 catch 절로 전송되어 throws 가 계속 될 것인지 여부를 결정한다.

패턴일 일치하지 않으면? → 마지막 catch 절로 이동하고 지역 error 상수에 바인딩 된다.

에러가 발생하지 않으면? → do 구문 아래에 나머지 구문들이 실행된다.

catch 절은 do 절에서 발생할 수 있는 모든 에러를 처리할 필요는 없다!

catch 절이 에러처리를 하지 않으면 에러는 주면에 throws 된다.

error를 catch로 처리를 하지 않고 전역 error로 넘어가게 설계할 수 있다.

## 추가 Switch - Case 로 Error Handling 하기

```swift
var juicemaker = JuiceMaker()
juicemaker.coinsDeposited = 2000

do {
    try juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
    print("쥬스 만들기 성공! 야미~")
} catch {
    switch error {
    case JuiceMakerError.invalidSelection :
        print("잘못된 선택 에러!")
    case JuiceMakerError.outOfStock:
        print("재고 없음 에러!")
    case JuiceMakerError.insufficientFunds(let coinNeeded):
        print("금액 부족 에러! \(coinNeeded) 필요!")
    default :
        print("알 수 없는 에러!")
    }
}
```

## 에러를 옵셔널 값으로 변환

### try?

- 에러를 옵셔널 값으로 변환하여 처리를 하기 위해 try? 를 사용한다.
- try? 표현식을 판별하는 동안 에러가 발생되면 이 표현식의 값은 nil 이다.
- 정상 동작 후에는 옵셔널 타입으로 정산 변환 값을 돌려받는다.

```swift
result = try? juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
result // Optional("수박 쥬스 만들기 성공!")
result = try? juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
result // nil
```

try? 를 사용하면 모든 에러를 같은 방식으로 처리하는 경우 간결하면 에러 처리 코드를 작성할 수 있다.

```swift
func fetchRecipe() -> Recipe? {
		if let recipe = try? fetchRecipeFrom본사() { return recipe }
		if let recipe = try? fetchRecipeFrom직영점() { return recipe }
		return nil
}
```

### try!

- throws 메서드가 실제로 런타임 에러를 발생하지 않는 다는 사실에 확신이 있다면?
- 이러한 경우엔 try!를 사용할 수 있고 에러를 발생하지 않는다고 호출을 래핑 할 수 잇습니다.
- 단! 에러가 발생한다면 런타임 에러가 일어납니다.

```swift
result = try! juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
result // Optional("수박 쥬스 만들기 성공!")
result = try! juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
// 런타임 오류 발생
```

# **Result Type**

Error 타입을 공부중에 Result Type이란 것을 들었는데,

없다, Swift Language Guide에 Error Handling 파트에는 없습니다,

[Developer - result](https://developer.apple.com/documentation/swift/result) 를 봐볼까요?

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfb14e38-a13c-4924-949c-5f1b36c9024c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfb14e38-a13c-4924-949c-5f1b36c9024c/Untitled.png)

`Errors` 분류에 `Result`가 포함되어 있습니다.

들어가서 보면

```
### Enumeration## Result

A value that represents either a success or a failure, including an associated value in each case.

```

Markdown

Copy

enum 으로 구현된 `Result` 라는 친구를 볼 수 있어요

## **선언**

```
@frozen enum Result<Success, Failure> where Failure : Error

```

Swift

Copy

🤔 … ? 아직 응애 iOS개발자는 이렇게 보여주면 몰라요

예제가 필요합니다…

[Error Handling](https://www.notion.so/Error-Handling-c39aa15c72bb4cc6b574e49ce10ee315)

에서 사용한 예제를 가져와 사용해보겠습니다!

## **기존 Error Handling 을 이용한 방법**

```
enum JuiceMakerError: Error {
    case invalidSelection
    case outOfStock
    case insufficientFunds(coinsNeeded: Int)
}

struct Juice {
    var amount: Int
    var price: Int
}

class JuiceMaker {
    var inventory = [
        "Strawberry Juice": Juice(amount: 500, price: 4500),
        "Kiwi Juice": Juice(amount: 300, price: 5000),
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

do {
    try juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
    print("쥬스 만들기 성공! 야미~")
} catch JuiceMakerError.invalidSelection {
    print("잘못된 선택 에러!")
} catch JuiceMakerError.outOfStock {
    print("재고 없음 에러!")
} catch JuiceMakerError.insufficientFunds(let coinNeeded) {
    print("금액 부족 에러! \(coinNeeded) 필요!")
} catch {
    print("알 수 없는 에러!")
}

```

Swift

Copy

## **Result Type을 적용한 방법**

```
enum JuiceMakerError: Error {
    case invalidSelection
    case outOfStock
    case insufficientFunds(coinsNeeded: Int)
}

struct Juice {
    var amount: Int
    var price: Int
}

class JuiceMaker {
    var inventory = [
        "Strawberry Juice": Juice(amount: 500, price: 4500),
        "Kiwi Juice": Juice(amount: 300, price: 5000),
        "Watermelon Juice": Juice(amount: 1000, price: 3000)
    ]
    var coinsDeposited = 0

		//👇👇👇👇 Result 적용! 👇👇👇👇
    func makeJuiceForResult(juiceNamed name: String) -> Result<Bool, JuiceMakerError> {
        guard let juice = inventory[name] else {
            return .failure(.invalidSelection)
        }
        guard juice.amount > 0 else {
            return .failure(.outOfStock)
        }
        guard juice.price <= coinsDeposited else {
            return .failure(.insufficientFunds(coinsNeeded: juice.price - coinsDeposited))
        }

        return .success(true)
    }
		//👆👆👆👆👆👆👆👆👆👆👆👆👆👆👆👆👆
}

var juicemaker = JuiceMaker()
juicemaker.coinsDeposited = 2000

let isMakeable = juicemaker.makeJuiceForResult(juiceNamed: "Watermelon Juice")

switch isMakeable {
case .success(let data):
    print(data)
case .failure(let error):
    print(error)
}

```

Swift

Copy

## **차이점**

- 기존

```
func makeJuice(juiceNamed name: String) throws

```

Swift

Copy

- Result

```
func makeJuiceForResult(juiceNamed name: String) -> Result<Bool, JuiceMakerError>

```

Swift

Copy

기존 코드에서는 `throws` 를 통해 에러를 던져주고 `result` 를 이용한 경우에는 `Result type` 을 반환해 주고 있네요!

## **Result 사용법**

Result를 사용하려면 성공했을 경우와, 실패했을 경우의 값을 넣어줘야 합니다.

`Result<Bool, JuiceMakerError>` 이렇게요!

이렇게 넣어주면? →

- 성공 : Bool 타입인 true of false 로 받음
- 실패 : 미리 선언된 Error 열거형으로 받음

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8bf9ad38-2774-455f-a387-20ea0ea3c746/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8bf9ad38-2774-455f-a387-20ea0ea3c746/Untitled.png)

isMakeable은 Result 타입의 변수가 된다!

그래서 Result 타입은 `Result<Success, Failure>` 로 이루어져 있기 때문에 Switch Case 를 통해 경우에 따라 처리를 해주면 됩니다!

```
let isMakeable = juicemaker.makeJuiceForResult(juiceNamed: "Watermelon Juice")

switch isMakeable {
case .success(let data):
    print(data)
case .failure(let error):
    print(error)
}

```

Swift

Copy

이런식으로요!

### **참고**

[https://velog.io/@un1945/Swift-Result-Type](https://velog.io/@un1945/Swift-Result-Type)

[Result - developer.apple](https://developer.apple.com/documentation/swift/result)

---

# **Defer**

defer 구문은 현재 코드 블록을 나가기 전에 꼭 실행되야 하는 코드를 작성합니다.

코드가 블록을 어떻게 빠져 나가든 꼭 마무리해야 되는 작업을 할 수 있게 도와줍니다!

```
func greeting() {
		defer {
				print("안녕하세요~")
		}

		print("Hello World!")
}

// 실행결과
// Hello World!
// 안녕하세요~

```

Swift

Copy

이렇게 실행결과에서 볼 수 있듯이 defer는 greeting 함수가 끝나기 직전에 실행되는 모습을 볼 수 있습니다!

🤔 그렇다면 함수안에 defer 이 여려개가 있다면?

## **Defer 의 실행 순서**

```
func greeting() {
    defer {
        print("First Defer")
    }
    defer {
        print("Second Defer")
    }
    defer {
        print("Third Defer")
    }
    print("Hello World!")
}

// 실행결과
// Hello World!
// Third Defer
// Second Defer
// First Defer

```

Swift

Copy

이렇게 실행 결과에서 볼 수 있듯이 defer은 선언 된 역순으로 실행된다!

## **참고**

[https://swieeft.github.io/2020/02/26/defer.html](https://swieeft.github.io/2020/02/26/defer.html)

# ****🔥 오늘의 3줄 회고****

- Swift Guide는 들어갈 때마다 새로운 친구들이 나온다.
- 급할거 없다. 천천히 꼼꼼히 읽자
- 오늘의 기록은 오늘 기록!