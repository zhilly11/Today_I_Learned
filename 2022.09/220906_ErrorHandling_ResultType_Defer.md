# 220906_ErrorHandling_ResultType_Defer

# βοΈΒ TIL (Today I Learned)

# π₯Β μ€λμ λͺ©ν

- [x] μ₯¬μ€λ©μ΄μ»€ STEP-2 PR
- [x] λ¨Έμ± νλ μ€λΉ
- [ ] 


# ****π₯Β κ³΅λΆν λ΄μ©****

## Error Handling

- μλ¬μ²λ¦¬λ νλ‘κ·Έλ¨μ μλ¬ μ‘°κ±΄μμ μλ΅νκ³  λ³΅κ΅¬νλ νλ‘μΈμ€
- Swiftλ λ°νμμ λ³΅κ΅¬ κ°λ₯ν μλ¬λ₯Ό λμ§κ³  ν¬μ°©νκ³  μ ννκ³  μ‘°μνκΈ° μν μ΅κ³  μμ€μ μ§μμ νλ€.
- μΌλΆ μμμ ν­μ μ€νμ μλ£νκ±°λ μ μ©ν μΆλ ₯μ μμ±νλ€κ³  λ³΄μ₯νμ§ μλλ€.
- μ΅μλμ κ°μ΄ μμμ λνλ΄λλ° μ¬μ©λμ§λ§ μμμ΄ μ€ν¨ν  κ²½μ° μ½λκ° κ·Έμ λ°λΌ μλ΅ν  μ μλλ‘ μλ¬μ μμΈμ μ΄ν΄νλ κ²μ΄ μ μ©ν κ²½μ°κ° λ§λ€.

> NOTE
> 
> 
> Swiftμμ μλ¬ μ²λ¦¬λ Cocoaμ Objective-Cμ NSErrorλ₯Ό μ¬μ©νλ μλ¬ μ²λ¦¬ ν¨ν΄κ³Ό μνΈ μ΄μ©λλ€.
> 

## Representing and Throwing Errors

Swiftμμ μλ¬λ Error νλ‘ν μ½μ μ€μνλ νμμ κ°μΌλ‘ ννλλ€.

Swift μ΄κ±°νμ κ΄λ ¨λ μλ¬ μ‘°κ±΄μ κ·Έλ£Ήμ λͺ¨λΈλ§νλλ° νΉν μ ν©νλ©° κ΄λ ¨κ°μ μ¬μ©νμ¬ μλ¬μ νΉμ±μ λν μΆκ° μ λ³΄λ₯Ό μ λ¬ν  μ μλ€.

λ€μμ κ²μ λ΄μμ μ₯¬μ€ νλ§€κΈ°λ₯Ό μλνλ μλ¬ μ‘°κ±΄μ λνλ΄λ λ°©λ²μ΄λ€.

```swift
enum JuiceMakerError: Error {
    case invalidSelection
    case outOfStock
    case insufficientFunds(coinsNeeded: Int)
}
```

μλ¬κ° λ°μνλ©΄ μμμΉ λͺ»ν μΌμ΄ λ°μνμ¬ μ μμ μΈ νλ¦μ κ³μν  μ μμμ λνλΌ μ μλ€.

throw κ΅¬λ¬Έμ μ¬μ©νμ¬ μλ¬λ₯Ό λ°μ μν΅λλ€.

```swift
throw JuiceMakerError.insufficientFunds(coinsNeeded: 1000)
```

## Handling Errors

μλ¬κ° λ°μν  λ μ£Όλ³ μ½λμ λΆλΆμ΄ μλ¬ μ²λ¦¬λ₯Ό λ΄λΉν΄μΌ νλ€. μλ₯Ό λ€μ΄ λ¬Έμ λ₯Ό μμ νκ±°λ λ€λ₯Έ λ°©λ²μ μλνκ±°λ μ¬μ©μμκ² μλ¬λ₯Ό μλ¦¬λ λ°©λ²μΌλ‘ μλ¬ μ²λ¦¬λ₯Ό ν΄μΌνλ€.

Swiftμμλ μλ¬λ₯Ό μ²λ¦¬νλ 4κ°μ§ λ°©λ²μ΄ μλ€. ν¨μμμ ν΄λΉ ν¨μλ₯Ό νΈμΆνλ μ½λλ‘ μλ¬λ₯Ό μ ν νκ±°λ do - catch κ΅¬λ¬Έμ μ¬μ©νκ±°λ μ΅μλ κ°μΌλ‘ μλ¬λ₯Ό μ²λ¦¬νκ±°λ μλ¬κ° λ°μνμ§ μμ κ²μ΄λΌκ³  μ£Όμ₯ν  μ μλ€.

ν¨μμμ μλ¬κ° λ°μνλ©΄ νλ‘κ·Έλ¨μ νλ¦μ΄ λ³κ²½λλ―λ‘ μ½λμμ μλ¬κ° λ°μν  μ μλ μμΉλ₯Ό μ μνκ² μ μ μμ΄μΌ νλ€. μ½λμμ μ΄λ¬ν μμΉλ₯Ό μλ³νλ €λ©΄ μλ¬κ° λ°μν  μ μλ ν¨μ, λ©μλ, λλ μ΄κΈ°ν κ΅¬λ¬Έ νΈμΆνλ μ½λ μ΄μ μ try λλ try? λλ try! ν€μλλ₯Ό μμ±ν΄μΌ νλ€.

## throw ν¨μλ₯Ό μ΄μ©ν μλ¬ μ ν

μλ¬κ° λ°μν  μ μλ ν¨μ, λ©μλ, λλ μ΄κΈ°ν κ΅¬λ¬Έμ λνλ΄κΈ° μν΄ νλΌν€λ λ€μ ν¨μμ μ μΈμ throwν€μλλ₯Ό μμ±ν΄ μ€λλ€!

```swift
func makeJuice(juiceNamed name: String) throws
```

throwν¨μλ λ΄λΆμμ λ°μν μλ¬λ₯Ό νΈμΆλ λ²μλ‘ μ νν©λλ€.

> NOTE
> 
> 
> throw ν¨μλ μλ¬λ§ μ ν ν  μ μμ΅λλ€. throwμ μΈμ΄ λμ§ μμ ν¨μ λ΄μμ λ°μλ λͺ¨λ  μλ¬λ ν¨μ λ΄μμ μ²λ¦¬ν΄μΌνλ€.
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
        
        print("\(name) λμμ΅λλ€~")
    }
}
```

μμ λ₯Ό λ³΄μ.

`makeJuice(juiceNamed:)` λ©μλμ κ΅¬νμ `guard` κ΅¬λ¬Έμ μ¬μ©νμ¬ λ©μλλ₯Ό μΌμ° μ’λ£μν€κ³  wbtm κ΅¬λ§€ μκ΅¬μ¬ν­ μ€ νλλΌλ μΆ©μ‘±νμ§ μμΌλ©΄ μ μ ν μλ¬λ₯Ό λ°μν©λλ€. `throw`κ΅¬λ¬Έμ νλ‘κ·Έλ¨ μ μ΄λ₯Ό μ¦μ μ λ¬νλ―λ‘ ν­λͺ©μ μκ΅¬μ¬ν­μ΄ λͺ¨λ λ§μ‘±ν΄μΌλ§ νλ§€λ©λλ€.

`makeJuice(juiceNamed:` λ©μλλ λ°μνλ μλ¬λ₯Ό μ ννκΈ° λλ¬Έμ μ΄ λ©μλλ₯Ό νΈμΆνλ μ½λλ do-catch κ΅¬λ¬Έ, tryλ₯Ό μ¬μ©νμ¬ μλ¬λ₯Ό μ²λ¦¬νκ±°λ κ³μ μ νν΄μΌνλ€!

```swift
func sendToErrorJuice() throws {
			try JuiceMaker.makeJuice("kiwiJuice")
}
```

μ΄λ°μμΌλ‘ throws λ₯Ό λ°μ λ€μ ν λ²λ throws μν¬ μ μλ€!

## Do - Catch μ¬μ©νμ¬ μλ¬ μ²λ¦¬νκΈ°

do - catch κ΅¬λ¬Έμ μ¬μ©νμ¬ μ½λμ λΈλ­μ μ€ννμ¬ μλ¬λ₯Ό μ²λ¦¬νλ€!

μλ¬κ° do μ μμ λ°μλλ©΄ catch μ κ³Ό λΉκ΅νμ¬ μλ¬λ₯Ό μ²λ¦¬ν  μ μλ ν­λͺ©μ κ²°μ νλ€.

```swift
do {
		try ((throws κ΅¬λ¬Έ))
		((code))
} catch ((error.name1)) {
		((code))
} catch ((error.name2)) where ((μ‘°κ±΄λ¬Έ)) {
		((code))
} catch ((error.name3)), ((error.name4)) {
		((code))
} catch {
		((code))
}
```

μ²λ¦¬ν  μ μλ μλ¬κ° λ¬΄μμΈμ§ λνλ΄κΈ° μν΄ catch λ€μ ν¨ν΄μ μμ±ν©λλ€.

catch μ μ΄ ν¨ν΄μ κ°μ§κ³  μμ§ μλ€λ©΄ μ΄ μ μ λͺ¨λ  μλ¬μ μΌμΉνκ³  error λΌλ μ΄λ¦μ κ°μ§ μ§μ­ μμλ‘ μλ¬λ₯Ό λ°μΈλ ν©λλ€.

```swift
var juicemaker = JuiceMaker()
juicemaker.coinsDeposited = 2000

do {
    try juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
    print("μ₯¬μ€ λ§λ€κΈ° μ±κ³΅! μΌλ―Έ~")
} catch JuiceMakerError.invalidSelection {
    print("μλͺ»λ μ ν μλ¬!")
} catch JuiceMakerError.outOfStock {
    print("μ¬κ³  μμ μλ¬!")
} catch JuiceMakerError.insufficientFunds(let coinNeeded) {
    print("κΈμ‘ λΆμ‘± μλ¬! \(coinNeeded) νμ!")
} catch {
    print("μ μ μλ μλ¬!")
}

// Prints "κΈμ‘ λΆμ‘± μλ¬! 1000 νμ!"
```

μμ μμ μμ `makeJuice(juiceNamed:)` λ errorλ₯Ό λ°μν  μ μμΌλ―λ‘ try ννμμΌλ‘ νΈμΆ λλ€.

μλ¬κ° λ°μνλ©΄ μ€νμ΄ μ¦μ catch μ λ‘ μ μ‘λμ΄ throws κ° κ³μ λ  κ²μΈμ§ μ¬λΆλ₯Ό κ²°μ νλ€.

ν¨ν΄μΌ μΌμΉνμ§ μμΌλ©΄? β λ§μ§λ§ catch μ λ‘ μ΄λνκ³  μ§μ­ error μμμ λ°μΈλ© λλ€.

μλ¬κ° λ°μνμ§ μμΌλ©΄? β do κ΅¬λ¬Έ μλμ λλ¨Έμ§ κ΅¬λ¬Έλ€μ΄ μ€νλλ€.

catch μ μ do μ μμ λ°μν  μ μλ λͺ¨λ  μλ¬λ₯Ό μ²λ¦¬ν  νμλ μλ€!

catch μ μ΄ μλ¬μ²λ¦¬λ₯Ό νμ§ μμΌλ©΄ μλ¬λ μ£Όλ©΄μ throws λλ€.

errorλ₯Ό catchλ‘ μ²λ¦¬λ₯Ό νμ§ μκ³  μ μ­ errorλ‘ λμ΄κ°κ² μ€κ³ν  μ μλ€.

## μΆκ° Switch - Case λ‘ Error Handling νκΈ°

```swift
var juicemaker = JuiceMaker()
juicemaker.coinsDeposited = 2000

do {
    try juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
    print("μ₯¬μ€ λ§λ€κΈ° μ±κ³΅! μΌλ―Έ~")
} catch {
    switch error {
    case JuiceMakerError.invalidSelection :
        print("μλͺ»λ μ ν μλ¬!")
    case JuiceMakerError.outOfStock:
        print("μ¬κ³  μμ μλ¬!")
    case JuiceMakerError.insufficientFunds(let coinNeeded):
        print("κΈμ‘ λΆμ‘± μλ¬! \(coinNeeded) νμ!")
    default :
        print("μ μ μλ μλ¬!")
    }
}
```

## μλ¬λ₯Ό μ΅μλ κ°μΌλ‘ λ³ν

### try?

- μλ¬λ₯Ό μ΅μλ κ°μΌλ‘ λ³ννμ¬ μ²λ¦¬λ₯Ό νκΈ° μν΄ try? λ₯Ό μ¬μ©νλ€.
- try? ννμμ νλ³νλ λμ μλ¬κ° λ°μλλ©΄ μ΄ ννμμ κ°μ nil μ΄λ€.
- μ μ λμ νμλ μ΅μλ νμμΌλ‘ μ μ° λ³ν κ°μ λλ €λ°λλ€.

```swift
result = try? juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
result // Optional("μλ° μ₯¬μ€ λ§λ€κΈ° μ±κ³΅!")
result = try? juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
result // nil
```

try? λ₯Ό μ¬μ©νλ©΄ λͺ¨λ  μλ¬λ₯Ό κ°μ λ°©μμΌλ‘ μ²λ¦¬νλ κ²½μ° κ°κ²°νλ©΄ μλ¬ μ²λ¦¬ μ½λλ₯Ό μμ±ν  μ μλ€.

```swift
func fetchRecipe() -> Recipe? {
		if let recipe = try? fetchRecipeFromλ³Έμ¬() { return recipe }
		if let recipe = try? fetchRecipeFromμ§μμ () { return recipe }
		return nil
}
```

### try!

- throws λ©μλκ° μ€μ λ‘ λ°νμ μλ¬λ₯Ό λ°μνμ§ μλ λ€λ μ¬μ€μ νμ μ΄ μλ€λ©΄?
- μ΄λ¬ν κ²½μ°μ try!λ₯Ό μ¬μ©ν  μ μκ³  μλ¬λ₯Ό λ°μνμ§ μλλ€κ³  νΈμΆμ λν ν  μ μμ΅λλ€.
- λ¨! μλ¬κ° λ°μνλ€λ©΄ λ°νμ μλ¬κ° μΌμ΄λ©λλ€.

```swift
result = try! juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
result // Optional("μλ° μ₯¬μ€ λ§λ€κΈ° μ±κ³΅!")
result = try! juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
// λ°νμ μ€λ₯ λ°μ
```

# **Result Type**

Error νμμ κ³΅λΆμ€μ Result Typeμ΄λ κ²μ λ€μλλ°,

μλ€, Swift Language Guideμ Error Handling ννΈμλ μμ΅λλ€,

[Developer - result](https://developer.apple.com/documentation/swift/result)Β λ₯Ό λ΄λ³ΌκΉμ?

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfb14e38-a13c-4924-949c-5f1b36c9024c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfb14e38-a13c-4924-949c-5f1b36c9024c/Untitled.png)

`Errors`Β λΆλ₯μΒ `Result`κ° ν¬ν¨λμ΄ μμ΅λλ€.

λ€μ΄κ°μ λ³΄λ©΄

```
### Enumeration## Result

A value that represents either a success or a failure, including an associated value in each case.

```

Markdown

Copy

enum μΌλ‘ κ΅¬νλΒ `Result`Β λΌλ μΉκ΅¬λ₯Ό λ³Ό μ μμ΄μ

## **μ μΈ**

```
@frozen enum Result<Success, Failure> where Failure : Error

```

Swift

Copy

π€Β β¦ ? μμ§ μμ  iOSκ°λ°μλ μ΄λ κ² λ³΄μ¬μ£Όλ©΄ λͺ°λΌμ

μμ κ° νμν©λλ€β¦

[Error Handling](https://www.notion.so/Error-Handling-c39aa15c72bb4cc6b574e49ce10ee315)

μμ μ¬μ©ν μμ λ₯Ό κ°μ Έμ μ¬μ©ν΄λ³΄κ² μ΅λλ€!

## **κΈ°μ‘΄ Error Handling μ μ΄μ©ν λ°©λ²**

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

        print("\(name) λμμ΅λλ€~")
    }
}

do {
    try juicemaker.makeJuice(juiceNamed: "Watermelon Juice")
    print("μ₯¬μ€ λ§λ€κΈ° μ±κ³΅! μΌλ―Έ~")
} catch JuiceMakerError.invalidSelection {
    print("μλͺ»λ μ ν μλ¬!")
} catch JuiceMakerError.outOfStock {
    print("μ¬κ³  μμ μλ¬!")
} catch JuiceMakerError.insufficientFunds(let coinNeeded) {
    print("κΈμ‘ λΆμ‘± μλ¬! \(coinNeeded) νμ!")
} catch {
    print("μ μ μλ μλ¬!")
}

```

Swift

Copy

## **Result Typeμ μ μ©ν λ°©λ²**

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

		//ππππ Result μ μ©! ππππ
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
		//πππππππππππππππππ
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

## **μ°¨μ΄μ **

- κΈ°μ‘΄

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

κΈ°μ‘΄ μ½λμμλΒ `throws`Β λ₯Ό ν΅ν΄ μλ¬λ₯Ό λμ Έμ£Όκ³ Β `result`Β λ₯Ό μ΄μ©ν κ²½μ°μλΒ `Result type`Β μ λ°νν΄ μ£Όκ³  μλ€μ!

## **Result μ¬μ©λ²**

Resultλ₯Ό μ¬μ©νλ €λ©΄ μ±κ³΅νμ κ²½μ°μ, μ€ν¨νμ κ²½μ°μ κ°μ λ£μ΄μ€μΌ ν©λλ€.

`Result<Bool, JuiceMakerError>`Β μ΄λ κ²μ!

μ΄λ κ² λ£μ΄μ£Όλ©΄? β

- μ±κ³΅ : Bool νμμΈ true of false λ‘ λ°μ
- μ€ν¨ : λ―Έλ¦¬ μ μΈλ Error μ΄κ±°νμΌλ‘ λ°μ

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8bf9ad38-2774-455f-a387-20ea0ea3c746/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8bf9ad38-2774-455f-a387-20ea0ea3c746/Untitled.png)

isMakeableμ Result νμμ λ³μκ° λλ€!

κ·Έλμ Result νμμΒ `Result<Success, Failure>`Β λ‘ μ΄λ£¨μ΄μ Έ μκΈ° λλ¬Έμ Switch Case λ₯Ό ν΅ν΄ κ²½μ°μ λ°λΌ μ²λ¦¬λ₯Ό ν΄μ£Όλ©΄ λ©λλ€!

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

μ΄λ°μμΌλ‘μ!

### **μ°Έκ³ **

[https://velog.io/@un1945/Swift-Result-Type](https://velog.io/@un1945/Swift-Result-Type)

[Result - developer.apple](https://developer.apple.com/documentation/swift/result)

---

# **Defer**

defer κ΅¬λ¬Έμ νμ¬ μ½λ λΈλ‘μ λκ°κΈ° μ μ κΌ­ μ€νλμΌ νλ μ½λλ₯Ό μμ±ν©λλ€.

μ½λκ° λΈλ‘μ μ΄λ»κ² λΉ μ Έ λκ°λ  κΌ­ λ§λ¬΄λ¦¬ν΄μΌ λλ μμμ ν  μ μκ² λμμ€λλ€!

```
func greeting() {
		defer {
				print("μλνμΈμ~")
		}

		print("Hello World!")
}

// μ€νκ²°κ³Ό
// Hello World!
// μλνμΈμ~

```

Swift

Copy

μ΄λ κ² μ€νκ²°κ³Όμμ λ³Ό μ μλ―μ΄ deferλ greeting ν¨μκ° λλκΈ° μ§μ μ μ€νλλ λͺ¨μ΅μ λ³Ό μ μμ΅λλ€!

π€ κ·Έλ λ€λ©΄ ν¨μμμ defer μ΄ μ¬λ €κ°κ° μλ€λ©΄?

## **Defer μ μ€ν μμ**

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

// μ€νκ²°κ³Ό
// Hello World!
// Third Defer
// Second Defer
// First Defer

```

Swift

Copy

μ΄λ κ² μ€ν κ²°κ³Όμμ λ³Ό μ μλ―μ΄ deferμ μ μΈ λ μ­μμΌλ‘ μ€νλλ€!

## **μ°Έκ³ **

[https://swieeft.github.io/2020/02/26/defer.html](https://swieeft.github.io/2020/02/26/defer.html)

# ****π₯Β μ€λμ 3μ€ νκ³ ****

- Swift Guideλ λ€μ΄κ° λλ§λ€ μλ‘μ΄ μΉκ΅¬λ€μ΄ λμ¨λ€.
- κΈν κ±° μλ€. μ²μ²ν κΌΌκΌΌν μ½μ
- μ€λμ κΈ°λ‘μ μ€λ κΈ°λ‘!