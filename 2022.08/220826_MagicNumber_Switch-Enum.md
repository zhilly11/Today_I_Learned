# โ๏ธย TIL (Today I Learned)

# ๐ฅย ์ค๋์ ๋ชฉํ

- [ ]  ๋ฌต์ฐ๋น  STEP-2 ๋ฆฌํฉํ ๋ง
- [ ]  ๋ฌต์ฐ๋น  STEP-2 ๋ฆฌ๋๋ฏธ ์์ฑ
- [ ]  

# ๐ฅย ์ค๋ ํ ์ผ & ๊ณต๋ถํ ๋ด์ฉ

## ๋ฌต์ฐ๋น  readme ์์ฑ

## README ์์ฑ์ tree๋ฅผ ํํํ  ๋๋ ์ฝ๋๋ธ๋ญ์ผ๋กํด์ bash์ธ์ด๋ก ์ค์ ํ๋ฉด ๋๋ค

```bash
.
โโโ Case
โย ย  โโโ RockPaperScissorCase.swift
โย ย  โโโ TurnCase.swift
โย ย  โโโ WinLoseDrawCase.swift
โโโ Library
โย ย  โโโ RockPaperScissorsLibrary.swift
โโโ Protocol
โย ย  โโโ RockPaperScissorsLibraryProtocol.swift
โโโ main.swift

```

## ๋งค์ง๋๋ฒ

์์๋ก ์ ์ธํ์ง ์๋ ์ซ์, ๋ฌธ์์ด์ ๋งค์ง๋๋ฒ or ๋งค์ง๋ฆฌํฐ๋ด ์ด๋ผ๊ณ  ํ๋ค.

```swift
if userHand == 1 && computerHand == 3 {
        print("user ์น๋ฆฌ!")
}

```

๊ฐ๋จํ ๊ฐ์๋ฐ์๋ณด ์์ ์ด๋ค ์ฌ๊ธฐ์ ๋ณด๋ฉด userHand์ computerHand๊ฐ ์ด๋ค ๊ฐ์ ๊ฐ๋ฆฌํค๋์ง ์ ์ ์๋ค. ์ด๋ฐ ๊ฒ์ ๋ณดํต ์ฐ๋ฆฐ ๋งค์ง ๋๋ฒ๋ผ๊ณ  ๋ถ๋ฅธ๋ค. ๊ทธ๋ ๋ค๋ฉด ์ด๋ป๊ฒ ์ข์ ์ฝ๋๋ก ์์ ํ  ์ ์์๊น?

```swift
enum HandCase {
    case rock
    case scissor
    case paper
}

if userHand == .rock && computerHand == .scissor {
    print("user ์น๋ฆฌ..!")
}

```

swift์์๋ enum์ผ๋ก ์ผ์ด์ค๋ฅผ ๋ง๋ค์ด ๋ณด๊ธฐ ์ข์ ์ฝ๋๋ก ์์ ํด ์ค ์ ์๋ค..!

## tuple์ ์ด์ฉํ switch๋ฌธ

```
let bothHands = (userHand, computerHand)

switch bothHands {
case let (userHand, computerHand) where userHand == computerHand:
        return .draw
case (.scissor, .paper):
        return .win
case (.rock, .scissor):
        return .win
case (.paper, .rock):
        return .win
default:
        return .lose
        }

```

swift์ control flow ์ค switch ๋ฌธ์์๋ ํํ์ ๋น๊ต ๊ฐ์ผ๋ก ์ฌ์ฉํ  ์ ์๋ค!
value binding๋ ๊ฐ๋ฅํ๋ ์ฌ๋ฌ๊ฐ์ง ๋ฐฉ๋ฒ์ผ๋ก ์ฌ์ฉํ  ์ ์์ ๊ฒ ๊ฐ๋ค.

# ****๐ฅย ์ค๋์ 3์ค ํ๊ณ ****

- ๋ฌต์ฐ๋น ํ  ๋๋ง๋ค ์๊ฐ๋  ํ๋ก์ ํธ^&^
- ํ๋ก์ ํธ๊ฐ ๋๋ ๋๋ง๋ค ๋ง์๊ฒ์ ๋ฐฐ์์ ๋๋๋ค
- ์กธ ๋ ค
