# Today_I_Learned

## View의 LifeCycle

![https://i.imgur.com/EGtGZlT.png](https://i.imgur.com/EGtGZlT.png)

ViewController는 위와 같은 Life Cycle을 가진다.

차근 차근 봐볼까요

# View가 화면에 나타나는 과정

먼저 ViewContoller가 `init`이 되면! (근데 넌 어디서 init 되는거니… 알려줘 애플.. )

`loadView` 가 먼저 실행 된다! ( ViewController가 메모리에 할당 되었다?)

`viewDidLoad` 실행! (View가 Load 되었다?)

`viewWillAppear` 실행! (View가 나타날 것이다!)

`viewDidAppear` 실행! (View가 나타났다!)

까지가! ViewController가 화면에 나타나게 되는 과정입니다.

## View가 화면에서 사라지는 과정

`viewWillDisappear` 실행! (View 가 곧 사라질 것이다!)

`viewDidDisappear` 실행! (View가 사라졌다!)

`viewDidUnload` 실행! (View 메모리 로드 해제)

까지가 ViewCotroller 가 화면에서 사라지고 메모리 해제 되는 과정입니다.

## 그러나!

사실 기본적으로 Xcode에서 App project 를 만들게 되면 `viewDidLoad` 친구는 보이는데 다른 친구들은 안보이죠?

```
class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        debugPrint("Second viewDidLoad")
    }

    override func viewWillAppear(_ animated: Bool) {
        debugPrint("Second viewWillAppear")
    }

    override func viewDidAppear(_ animated: Bool) {
        debugPrint("Second viewDidAppear")
    }

    override func viewWillDisappear(_ animated: Bool) {
        debugPrint("Second viewWillDisappear")
    }

    override func viewDidDisappear(_ animated: Bool) {
        debugPrint("Second viewDidDisappear")
    }
}

```

이런 식으로 기본적으로 생략되어있던 메서드 들을 override 해서 맘대로 쓸 수 있답니다 👏

## 그러면!

저는 아직 애송이니까 항상 예제를 만들어 봐야해요

다음은 [야곰닷넷](https://yagom.net/courses/ios-starter-uikit/) 에서 만들어 봤던 예제를 가지고 test 해보겠습니다~
먼저 각 ViewController에 위의 예제 처럼 State Method를 override 해서 작성 해줬습니다.

![https://i.imgur.com/9XpKNxj.png](https://i.imgur.com/9XpKNxj.png)

![https://i.imgur.com/1hNbj62.png](https://i.imgur.com/1hNbj62.png)

### 앱 실행

앱을 바로 실행 시키게 되면

viewDidLoad -> viewWillAppear -> viewDidAppear 순으로 출력이 됩니다!

여기 까지 되면 View가 화면에 나타 났다는 뜻이겠죠?

### 두번째 화면 이동

show 방식으로 연결해둔 버튼을 눌러 Second ViewController로 화면 이동을 해볼까요?
(화면을 full로 채우는 방식 기준 설명입니다!)
(full로 채우는 방식이 아닌 건 추후 설명)

![https://i.imgur.com/gwWavV8.png](https://i.imgur.com/gwWavV8.png)

위에 그림처럼!

두번째 View가 Load 되면? -> Second `ViewDidLoad`

첫번째 View는 사라질 것이다~ -> First `viewWillDisAppear`

두번째 View가 곧 나타날 것이다~ -> `Second ViewWillAppear`

첫번째 View가 사라졌다! -> `First viewDidDisAppear`

두번째 View가 나타났다! -> `Second viewDidAppear`

이렇게 번갈아가며 순서가 진행되는 모습을 볼 수 있어요~

### 두번째 화면을 종료하고 첫번째 화면으로 가면?

![https://i.imgur.com/GJC4MA2.png](https://i.imgur.com/GJC4MA2.png)

두번째 View가 곧 사라질 것이다 -> Second viewWillDisappear

첫번째 View가 곧 나타날 것이다 -> First viewWillAppear

두번째 View가 사라졌다! -> Second viewDidDisappear

첫번재 View가 나타났다! -> First viewDidAppear

## 어라?

두번째 View가 사라지고 첫번재 View가 다시나타날 때에는 첫 번째 View가 viewDidLoad 되지 않았네요?

vieDidLoad는 화면이 처음 만들어질 때 한 번만 실행 됩니다. 따라서 두번째 화면 이동을 할 때 ViewDidUnLoad 되지 않고 얌전히 화면에서만 사라지고 잘 살아있었습니다!

# ****🔥 공부한 내용****

## ViewLifeCycle

## Step-3 리뷰에 대한 공부

## 

# ****🔥 문제점 → 해결 방법****

## ViewController에서 Model에 있는 Class를 과연 어느 State Method에서 할당할 것인가?

 참 오래 생각했던 문제점이였다.
 
 일단 알아야 할 것이 있다. StateMethod에서 loadView와 viewDidLoad는 사실 View Managing에 관련된 친구들이다.
 
 따라서 내가 고민하던 JuiceMaker를 어디서 할당해줘야 할지 문제는 사실 JuiceMaker가 View State에 따라 달라지는 친구였다면 유의미한 고민이였겠지만
 
 우리의 JuiceMaker 친구는 View Managing에 관련이 없는 친구이기 때문에! 원래 했던대로 쓰는게 맞다~
 
 그리고 만약에 View Managing에 관련이 있는 Class를 할당해줘야 한다? 이럴경우엔 미리 선언은 해주되 할당은 State Method 에서 해주는게 맞다고 생각이 든다. (비록 옵셔널 바인딩이 귀찮더라도,,,)
 
 Thanks for 수박!

# ****🔥 오늘의 3줄 회고****

- 질문을 두려워하지 말자
- 항상 내가 쓰는 코드에 대해서 이유를 말할 수 있어야 한다.
- 근거도 있어야 한다! 근거가 공식문서라면 내 빽은 Apple
