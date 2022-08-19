# 220818_Optional

Date: 2022년 8월 18일
Tag: Optional, Swift, iOS, 야곰

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [x]  짝프로그래밍 규칙 확실하게
- [x]  STEP 1 리뷰받은 부분 수정
- [x]  STEP 2 완료하고 PR 보내기

# 🔥 오늘 한 일

## 1. 숫자야구 STEP-1 리팩토링

## 2. 숫자야구 STEP-2 완료 후 PR

## 3. Optional 학습 활동

# ****🔥 공부한 내용****

## 1. Git 원격 Repositories 가져오는법

```
$ git clone http://~원격 Repo 주소~

$ git remote add upstream http://~원격 Repo 주소~

$ git fetch upstream

$ git checkout -t remotes/upstream/브랜치이름
```

## 2. Git add, commit, push한 내용 삭제하는 법

- Github 서버에 push한 commit을 삭제하는 방법은 다음과 같다.

```
// 삭제할 commit 확인
$ git log

// 가장 마지막에 push한 commit을 지우고 싶기 때문에 HEAD를 설정해 준다.
$ git reset HEAD^

// 마지막으로 push를 해줘서 Github에게도 commit을 삭제하도록 한다.
$ git push -f origin 브랜치명
```

## 3. Optional을 안전하게 Unwrapping 하는 방법

- Optional Binding, Optional Chaining, 강제 Unwrapping, 닐 병합 연산자.
- 활동 학습 시간에 Optional Binding을 정리했다.
- 시간이 나는대로 블로그에 포스팅 해보자.

### Optional

옵셔널은 ?를 써서 사용한다.

- 사용법

```swift
let shortForm: Int? = Int("42")
let longForm: Optional<Int> = Int("42")

```

- Optional.non은 nil을
- Optional.some(42) 은 랩핑된 값 42를

```swift
let number: Int? = Optional.some(42)
let noNumber: Int? = Optional.none
print(noNumber == nil)
// Prints "true"

```

Swift는 Optional을 안전하게 언래핑 할 수 있는 몇가지 방법을 제공한다.

### Optional Binding

: Apple이 제시하는 방법에는 3가지 방법이 있다.

(래핑된 값을 조건부로 바인딩 하려면 인스턴스를 새로운 변수로 변환해서 사용해야합니다.)

```swift
let optionalZhilly: String? = String("zhilly")

// 1. if let
// if let은 분기처리할 때 유용
if let zhilly = optionalZhilly {
    print(zhilly)
} else {
    print("Fail ㅠㅠ")
}

// 2. guard let
// guard let은 예외처리할 때 유용
func optionalBinding() {
    guard optionalZhilly != nil else {
        print("fail")
        return
    }
}
optionalBinding()

//3. switch
let optionalInt = Optional(11)
switch optionalInt {
case 0:
    print("0")
case 11:
    print("11")
default:
    print("nil")
}
```

## 4. Int == Optional(Int) 는 어떻게 성공적으로 빌드 될까?

- Apple 공식문서를 찾아보자
    
    You can also use this operator to compare a non-optional value to an optional that wraps the same type. The non-optional value is wrapped as an optional before the comparison is made. In the following example, the `numberToMatch` constant is wrapped as an optional before comparing to the optional `numberFromString`:
    
- 간단하게 번역하자면 옵셔널 타입이 아닌 값들은 비교되기전에 래핑이 된다고 한다.

예제 소스를 보자.

```swift
let numberToFind: Int = 23
let numberFromString: Int? = Int("23")      // Optional(23)
if numberToFind == numberFromString {    
	print("It's a match!")
}
// Prints "It's a match!"
```

따라서 `print("It's a match!")` 가 출력된다!

## 4. Foundation의 역할

- Foundation은 프레임워크로서, 원시 데이터 타입 사용(Number, Data, String), Collection(Array, Dictionary, Set) 등과 같은 컬렉션 타입 사용이 가능한 기능을 가지고 있다.
- 기본적으로는 스위프트 표준 라이브러리에서 가능한 것들이 있고, Foundation을 import하면 Apple에서 미리 만들어놓은 추가적인 기능들을 사용할 수 있다.

## 5. Swift Style Guide 에 의하면 한 줄에는 100글자를 기준으로 작성한다.

- Xcode → 설정 → page guide at column을 설정해 주었다.

# ****🔥 문제점 → 해결 방법****

## 1. 그냥 Git clone으로 가져오면 왜 branch까지 한번에 가져오지 않을까?

## 2. 언제 한 번 블로그를 통해 본적은 있지만 CLI로는 어떻게 실행할까?

```
// 사용법은 간단하다.

// 로컬에 클론해준다.
$ git clone http://~원격 Repo 주소~

// ~소스 수정~

// 변경사항을 stage area에 올려준다.
$ git add .

// commit 메세지를 작성해주고 commit!
$ git commit -m "커밋 메세지"

// 원격 서버에 push!
$ git push

// 원격 서버에 변경이 일어난 경우
$ git pull
```

- 자세한 문서는 [Git-Book](https://git-scm.com/book/ko/v2)을 참조하자!

## 3. Naming과 Convention에 관하여

- 숫자 야구 프로젝트를 진행할 때 제일 힘들었던 점인것 같다.
- [API Design Guidlines](https://swift.org/documentation/api-design-guidelines/)를 기준으로 잡고 기타 문서를 활용해 나만의 정리 문서를 만들어보자.

# ****🔥 오늘의 3줄 회고****

- 밤 늦게 까지 코딩은 역시 힘들다.. 그렇지만 재밌다… 아직까진
- 드디어 막막하던 공식문서를 활용할 수 있을 것 같다는 생각이 들었다.
- 이제는 옵셔널이 무섭지 않다. 줄여서 `이옵무않`

# TMI

활동학슴 중 우연히 본 coda의 터미널을 보고 나도 터미널 → iTerm으로 변경

변경후 예쁘장하게 커스텀 해 주었다.

![Untitled](220818_Optional%20b564f847fc74403389eb41a068930ca1/Untitled.png)

코딩할 맛이 산다… 참고하실분들은 [여기](https://ooeunz.tistory.com/21) 참고!!