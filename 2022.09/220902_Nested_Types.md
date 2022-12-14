# โ๏ธย TIL (Today I Learned)

# ๐ฅย ์ค๋์ ๋ชฉํ

- [x]  Nested Types ์ ๋ฆฌ
- [ ]  Error Handling, Result type ๊ณต๋ถ


# ๐ฅย ์ค๋ ํ ์ผ

### ์ฅฌ์ค๋ฉ์ด์ปค STEP-1 ์ต์ข ๋ฆฌํฉํฐ๋ง

### README Day!

# ****๐ฅย ๊ณต๋ถํ ๋ด์ฉ****

## Nested Types

์ด๊ฑฐํ์ ํน์  ํด๋์ค ๋๋ ๊ตฌ์กฐ์ฒด์ ๊ธฐ๋ฅ์ ์ง์ํ๊ธฐ ์ํด ์ฌ์ฉํ๋ค!

๋ ๋ณต์กํ ํ์์ ์ปจํ์คํธ ๋ด์์ ์ฌ์ฉํ๊ธฐ ์ํด ์์ํ๊ฒ ์ ํธ๋ฆฌํฐ ํด๋์ค์ ๊ตฌ์กฐ์ฒด๋ฅผ ์ ์ํ๋๊ฒ์ด ํธ๋ฆฌํ  ์ ์๋ค.

์ด๋ฅผ ์ํด Swift๋ Nested Types ๋ฅผ ์ ์ ํ  ์ ์์ผ๋ฉฐ ํ์์ ์ ์ ๋ด์์ ์ง์ํ๋ ์ด๊ฑฐํ, ํด๋์ค, ๊ตฌ์กฐ์ฒด๋ฅผ ์ค์ฒฉํ  ์ ์๋ค.

๋ค๋ฅธ ํ์ ๋ด์์ ์ค์ฒฉํ๋ ค๋ฉด ์ง์ํ๋ ํ์์ ์ธ๋ถ ์ค๊ดํธ ๋ด์ ์ ์๋ฅผ ์์ฑํด์ผ ํ๋ค.

## Nested Types์ ๋์

์๋ ์์ ๋ ์ฅฌ์ค ์ข๋ฅ์ ๋ฐ๋ผ ์ฅฌ์ค ๋ ์ํผ๋ฅผ ๊ฐ์ง๊ณ  ์๋ JuiceMaker ๋ผ๋ ํด๋์ค ์๋๋ค.

JuiceMaker ํด๋์ค๋ Fruit์ Juice๋ผ๋ ์ค์ฒฉ๋ ์ด๊ฑฐํ ๊ทธ๋ฆฌ๊ณ  displayRecipeํจ์๋ฅผ ๊ฐ์ง๊ณ  ์์ต๋๋ค!

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
            print("\(juice.fruit): \(juice.amount)๊ฐ ํ์")
        }
    }
}

```

์ฐจ๊ทผ์ฐจ๊ทผ ํ๋์ ๋ณด์ค๊น์?

```swift
class JuiceMaker {
    enum Fruit {
        case strawberry
        case banana
    }
...
```

๋จผ์  JuiceMaker ๋ผ๋ ํด๋์ค๋ฅผ ํ๋ ๋ง๋ค์ด ์คฌ์ต๋๋ค. ๊ทธ๋ฆฌ๊ณ  ์์ Fruit ๋ผ๋ enum์ ํ๋ ์์ฑํด ์ฃผ์์ต๋๋ค.

> Swift๋ *์ค์ฒฉ๋ ํ์ (nested types)*์ ์ ์ํ  ์ ์์ผ๋ฉฐ ์ง์ํ๋ ํ์์ ์ ์ ๋ด์์ ์ง์ํ๋ ์ด๊ฑฐํ, ํด๋์ค, ๊ทธ๋ฆฌ๊ณ  ๊ตฌ์กฐ์ฒด๋ฅผ ์ค์ฒฉํ  ์ ์์ต๋๋ค. ํ์์ ํ์ํ๋งํผ์ ์์ค์ผ๋ก ์ค์ฒฉ๋  ์ ์์ต๋๋ค.
> 

๋ผ๋ ๋ฌธ๊ตฌ๋ฅผ ํตํด ์ฐ๋ฆฌ๋ ์ง์ํ๋ ํ์์์์๋ ํ์ํ ์์ค๋งํผ! ์ด๊ฑฐํ, ํด๋์ค, ๊ตฌ์กฐ์ฒด๋ฅผ ์ค์ฒฉํ  ์ ์๋ค๋ ๊ฒ์ ์ ์ ์์ต๋๋ค.

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

๊ทธ ๋ฐ์ ๋๋ค๋ฅธ enum์ธ Juice๋ฅผ ์์ฑํด์ฃผ์์ต๋๋ค! 

Juice ์์๋ case๋ก ์ฃผ์ค ์ด๋ฆ๋ค์ด ์ ์๋์ด ์๊ณ  enum์์ Recipe๋ผ๋ ๊ตฌ์กฐ์ฒด๋ ๋ ์ ์ํด์ฃผ์๋ค์

```swift
func displayRecipe(selectJuice: Juice){
        for juice in selectJuice.recipe {
            print("\(juice.fruit): \(juice.amount)๊ฐ ํ์")
        }
}
```

JuiceMaker์์ ๋ฉ์๋๋ ๊ตฌํ๋์ด ์์ต๋๋ค! 

๊ตฌ์กฐ๋ฅผ ๋ณด๊ฒ ๋๋ฉด

```swift
class JuiceMaker
โโโ enum Fruit
โโโ enum Juice
โย ย  โโโ struct Recipe
โย ย  โโโ var recipe: [Recipe]
โโโ func displayRecipe(Juice)
```

์ด๋ฐ ์์ผ๋ก class ์์ enum ์์ struct, var ์ด ์ ์ ๋์ด ์์ต๋๋ค!

์ฌ๊ธฐ๊น์ง๊ฐ Nested Type ์์  Class ์์ต๋๋ค.

๊ทธ๋ ๋ค๋ฉด Juice ํด๋์ค์ ์ธ์คํด์ค๋ ์ด๋ป๊ฒ ์์ฑํ ๊น์?

```swift
var juiceMaker = JuiceMaker()
juiceMaker.displayRecipe(selectJuice: JuiceMaker.Juice.strawberryBananaJuice)
```

JuiceMaker๋ ํด๋์ค๋ผ ์์์  ์ด๋์๋ผ์ด์ฆ๊ฐ ์กด์ฌํฉ๋๋ค!

๋งค๊ฐ๋ณ์ ๋ถ๋ถ์ ๋ณด์๋ฉด JuiceMaker์ enum Juice์ .strawwberryBananaJuice ๊น์ง ํธ์ถ์ด ์ ๋๋๊ตฐ์!

```swift
// func displayRecipe ๊ฒฐ๊ณผ
strawberry: 10๊ฐ ํ์
banana: 1๊ฐ ํ์
Program ended with exit code: 0
```

## ์ฐธ๊ณ 

[Swift Language - Nested Types](https://docs.swift.org/swift-book/LanguageGuide/NestedTypes.html)

[https://zeddios.tistory.com/322](https://zeddios.tistory.com/322)

๋!

# ****๐ฅย ์ค๋์ 3์ค ํ๊ณ ****

- ์์ ๋ฅผ ๋ง๋ค์ด ๋ณด์. ํญ์
- ์ฝ๋์ ์ ๋ต์ ์๋ค. ์ง์ง
- ๊ธฐ๋ก์ ์ต๊ดํ ํ์. ์ ๋ฐ

