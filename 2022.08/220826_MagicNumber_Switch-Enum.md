# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  묵찌빠 STEP-2 리팩토링
- [ ]  묵찌빠 STEP-2 리드미 작성
- [ ]  

# 🔥 오늘 한 일 & 공부한 내용

## 묵찌빠 readme 작성

## README 작성시 tree를 표현할 때는 코드블럭으로해서 bash언어로 설정하면 된다

```bash
.
├── Case
│   ├── RockPaperScissorCase.swift
│   ├── TurnCase.swift
│   └── WinLoseDrawCase.swift
├── Library
│   └── RockPaperScissorsLibrary.swift
├── Protocol
│   └── RockPaperScissorsLibraryProtocol.swift
└── main.swift

```

## 매직넘버

상수로 선언하지 않는 숫자, 문자열을 매직넘버 or 매직리터럴 이라고 한다.

```swift
if userHand == 1 && computerHand == 3 {
        print("user 승리!")
}

```

간단한 가위바위보 예제이다 여기서 보면 userHand와 computerHand가 어떤 값을 가리키는지 알 수 없다. 이런 것을 보통 우린 매직 넘버라고 부른다. 그렇다면 어떻게 좋은 코드로 수정할 수 있을까?

```swift
enum HandCase {
    case rock
    case scissor
    case paper
}

if userHand == .rock && computerHand == .scissor {
    print("user 승리..!")
}

```

swift에서는 enum으로 케이스를 만들어 보기 좋은 코드로 수정해 줄 수 있다..!

## tuple을 이용한 switch문

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

swift의 control flow 중 switch 문에서는 튜플을 비교 값으로 사용할 수 있다!
value binding도 가능하니 여러가지 방법으로 사용할 수 있을 것 같다.

# ****🔥 오늘의 3줄 회고****

- 묵찌빠할 때마다 생각날 프로젝트^&^
- 프로젝트가 끝날때마다 많은것을 배움을 느낀다
- 졸 려
