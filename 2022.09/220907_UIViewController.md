# 220907_UIViewController

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  UIViewController 문서 학습
- [ ]  쥬스메이커 STEP-3 예습해보기
- [ ]  

# 🔥 오늘 한 일 & 공부한 내용

## UIViewConroller 문서 정리

## UIViewController 란?

UIKit App의 뷰 계층 구조를 관리하는 개체입니다!

## 정의

```swift
@MainActor class UIViewController : UIResponder
```

## 개요

UIViewController는 클래스의 모든 ViewController에 공통되는 공유 동작을 정의합니다.

UIViewController 클래스의 인스턴스를 생성하는 경우는 거의 없습니다.

대신 UIViewController를 하위 클래스로 분류하고 뷰 컨트롤러의 뷰 계층을 관리하는 데 필요한 메서드와 프로퍼티를 추가하세요.

View Controller의 주요 책임은 다음을 따릅니다.

- 일반적으로 기본 데이터에 대한 변경에 대한 응답으로 View 내용 업데이트
- View를 사용하여 사용자 상호작용에 응답
- View 크기 조정 및 전체 인터페이스 레이아웃 관리
- App 내의 다른 오브젝트와의 연계

View Controller는 뷰 계층에서 관리하는 뷰에 강하게 바인딩 되어 이벤트 처리에 관여합니다. 특히 View Controller는 객체이며 View Controller의 루트뷰와 해당 뷰의 슈퍼 뷰 사이의 응답자 체인에 삽입됩니다. 이러한 View Controller 는 일반적으로 다른 View Controller에 속합니다. View Controller의 View 중 이벤트를 처리하는 View가 없는 경우 View Controller는 이벤트를 처리하거나 슈퍼 뷰에 이벤트를 전달 할 수 있습니다.

View Controller는 거의 단독적응로 사용되지 않습니다. 대신, App의 사용자 인터페이스 일부를 소유한 여러 뷰 컨트롤러를 사용하는 경우가 많습니다. 예를 들어 한 View Controller는 항목 테이블을 표시하고 다른 View Controller 는 해당 테이블에서 선택한 항목을 표시할 수 있습니다. 

일반적으로 한 번에 하나의 View Controller 만 View에 표시됩니다. View Controller는 새로운 View set 를 표시하기 위해 다른 View Controller를 제공할 수도 있고 다른 View Controller의 콘텐츠를 위한 컨테이너로 기능하여 원하는 뷰에 애니메이션도 부여할 수 있습니다.

## Subclassing Note

모든 앱에는 UIView Controller 의 커스텀 Subclass 가 하나이상 포함되어 있습니다. 대부분 경우 앱에는 많은 Custom View Controller를 포함하고 있습니다. Custom View Controller는 앱의 모양과 사용자 상호 작용에 대한 반응 방식을 포함하여 앱의 전체 동작을 정의합니다. View Controller 사용 및 구현에 대한 자세한 내용은 [iOS용 컨트롤러 프로그래밍 가이드](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/index.html#//apple_ref/doc/uid/TP40007457)를 참조하세요.

### 뷰 관리

각 View Controller는 이 클래스의 속성에 저장되어 있는 뷰 게층을 관리합니다. Root View는 주로 View 계층의 나머지 부분에 대한 컨테이너 역할을 합니다. Root View의 크기와 위치는 Root View를 소유한 개체에 의해 결정됩니다. Window에 의해 소유되는 View Controller는 앱의 루트 View Controller이며 View의 크기는 window를 채울 수 있는 크기이다.

view controller는 소유한 view를 곧바로 로드하지 않습니다. view는 해당 프로퍼에 처음 액세스할때 로드 또는 생성됩니다. view controller의 view를 지정하는 방법에는 여러가지가 있습니다.

- [스토리보드](notion://www.notion.so/sagwa/etc/not-found)에 view controller와 view를 지정하세요. 스토리보드는 view를 지정하는 기본 방법입니다. 스토리보드를 사용해서 view와 view controller에 대한 해당 관계를 설정할 수 있습니다. 또한 view controller 사이의 관계와 하위 뷰를 지정하면 앱 동작을 보고 수정하는 것이 더 쉬워집니다.  스토리보드에서 view controller를 로드하려면 [UIStoryboard](notion://www.notion.so/sagwa/etc/not-found) 객체의 [instantiateViewController(withIdentifier :)](notion://www.notion.so/sagwa/etc/not-found) 메서드를 호출하십시오. UIStoryboard 객체는 view controller를 생성하여 코드에 반환합니다.
- [Nib 파일](notion://www.notion.so/sagwa/etc/not-found)을 사용하여 view controller에 대한 view를 지정하세요. nib 파일을 사용하면 단일 view controller의 view를 지정할 수 있지만 view controller 사이의 segue 또는 관계를 정의할 수는 없습니다. nib 파일은 view controller 자체에 대한 최소한의 정보만 저장합니다.  nib 파일을 사용하여 view controller 객체를 초기화하려면 view controller 클래스를 프로그래밍 방식으로 만들고 [init(nibName : bundle :)](notion://www.notion.so/sagwa/etc/not-found) 메서드를 사용하여 초기화하세요. view가 요청되면 view controller는 nib 파일에서 view를 로드합니다.
- [loadView()](notion://www.notion.so/sagwa/etc/not-found) 메서드를 사용하여 view controller의 view를 지정하세요. 이 방법에서는 뷰 계층 구조를 프로그래밍 방식으로 만들고 해당 계층 구조의 루트 뷰를 view controller의 view 프로퍼티에 할당합니다.

이러한 모든 방법은 적절한 view의 집합을 만들어 view 프로퍼티를 통해 노출한다는 점에서 같은 결과를 만들어냅니다.

<aside>
❗ 중요

view controller는 view와 view가 생성하는 모든 하위 뷰의 유일한 소유자입니다. 또한 view controller는 view를 생성하거나 (view controller 자체가 릴리즈 될 때와 같이) 소유권을 반환하는 일에 있어서 책임이 있습니다. view 객체를 스토리보드나 nib 파일에 저장하는 경우 각 view controller 객체는 view 객체를 요청받을때 자동적으로 해당 뷰의 사본을 가져옵니다.
하지만 view를 수동적으로 생성한다면 각 view controller는 반드시 고유한 view 집합을 소유하고 있어야 합니다. view controller간에는 view를 공유할 수 없습니다.

</aside>

view controller의 루트 뷰는 항상 할당된 공간에 딱 맞게 크기가 조정됩니다. 인터페이스 빌더를 통해 자동 레이아웃 제약 조건을 지정하면 계층 구조상의 각 view가 상위 뷰의 범위 내에서 배치되고 크기가 조정되는 방식을 제어할 수 있습니다. 또한 제약 조건을 프로그래밍적으로 생성하고 적절한 때에 추가하는 것도 가능합니다. 제약 조건을 만드는 방법에 대한 자세한 내용은 [자동 레이아웃 가이드](notion://www.notion.so/sagwa/etc/not-found)를 참조하십시오.

# 뷰 관련 Notification 처리

View가 나타나거나 사라지면 컨트롤러는 자동적으로 자체 메서드를 호출하여 하위 클래스가 변동사항에 응답할 수 있도록 합니다. [viewWillAppear(_ :)](notion://www.notion.so/sagwa/etc/not-found)와 같은 메서드를 사용하여 화면에 표시 할 뷰를 준비하고 [viewWillDisappear(_ :)](notion://www.notion.so/sagwa/etc/not-found)를 사용하여 변경 내용이나 다른 상태 정보를 저장합니다. 상황에 따라 적절한 메서드를 사용하세요.

그림 1은 view에서 가능한 visibility 상태와 상태 전환을 보여줍니다.
모든 'will' 콜백 메서드가 'done' 콜백 메서드와 쌍을 이루는 것은 아닙니다. 'will'콜백 메서드로 프로세스를 시작하면 해당 'did'와 반대 'will'콜백 메서드 모두에서 프로세스를 종료해야합니다.

![그림 1. 상태 전환 다이어그램](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b33a7b5b-390d-4db7-a2c3-16b1b9213f5c/Untitled.png)

그림 1. 상태 전환 다이어그램

# 뷰 회전 처리

iOS 8부터 모든 회전 관련 메서드는 더 이상 사용되지 않습니다. 대신에 회전은 view controller의 view 크기가 변경되는 이벤트로 간주되므로 [viewWillTransition(to:with:)](notion://www.notion.so/sagwa/etc/not-found) 메서드를 통해 보고됩니다. 인터페이스 방향이 변경되면 UIKit은 윈도우의 루트 view controller에서 이 메서드를 호출합니다. 그런 다음 해당보기 컨트롤러는 하위 view controller에 알리고 view controller 계층 전체에 메시지를 전파합니다.

iOS 6 및 iOS 7에서 앱은 Info.plist 파일에 정의된 인터페이스 방향을 지원합니다. view controller는 [supportedInterfaceOrientations](https://github.com/ESnark/sagwa/tree/6092cb95e077aa0abcc382e4e3b85a7e7fe9a670/not-found/README.md) 메서드를 오버라이드하여 지원하는 방향 리스트를 제한할 수 있습니다. 일반적으로 시스템은 이 메서드를 윈도우의 루트 view controller 또는 전체 화면을 채우기 위해 제공된 view controller에서만 호출합니다. 하위 view controller는 상위 view controller가 화면상에서 제공하는 부분을 사용할 뿐 회전모드의 지원 여부에는 영향을 줄 수 없습니다. 앱의 오리엔테이션 마스크와 view controller의 오리엔테이션 마스크의 교차점은 view controller를 어느 방향으로 회전시킬지 결정하는데 사용됩니다.

특정 방향으로 화면을 표시하고 싶은 경우 해당 view controller의 [preferredInterfaceOrientationForPresentation](notion://www.notion.so/sagwa/etc/not-found)를 오버라이드하면 됩니다.

표시중인 view controller에 대해 회전이 발생하면 [willRotate(to:datation:)](notion://www.notion.so/sagwa/etc/not-found), [willAnimateRotation(to:duration:)](notion://www.notion.so/sagwa/etc/not-found) 및 [doneRotate(from:)](notion://www.notion.so/sagwa/etc/not-found) 메서드가 회전 중에 호출됩니다. [viewWillLayoutSubviews()](notion://www.notion.so/sagwa/etc/not-found) 메서드는 view의 크기가 조정되고 상위 항목에 의해 배치된 후에 호출됩니다. 회전시 view controller가 표시되지 않으면 회전 메서드가 호출되지 않습니다. 그러나 view가 표시되는 중이라면 [viewWillLayoutSubviews()](notion://www.notion.so/sagwa/etc/not-found) 메서드가 호출됩니다. 이 메서드를 구현하면 [statusBarOrientation](notion://www.notion.so/sagwa/etc/not-found) 메서드를 호출하여 기기 방향을 결정할 수 있습니다.

<aside>
❗ 알림

앱이 시작될 때 앱은 반드시 세로 방향으로 인터페이스를 설정해야 합니다. 앱이 상술된 메커니즘에 따라 화면을 회전시키는 것은 [application(_:didFinishLaunchingWithOptions:)](notion://www.notion.so/sagwa/etc/not-found)가 값을 리턴한 이후부터 적용됩니다.

</aside>

## 컨테이너 뷰 컨트롤러 구현

UIViewController의 하위 커스텀 클래스는 컨테이너 뷰 컨트롤러로도 동작할 수 있습니다. 컨테이너 뷰 컨트롤러는 소유한 하위 view controller에 대한 컨텐츠 표시를 관리합니다. 하위 view는 그대로 표시되거나 컨테이너 뷰 컨트롤러가 소유한 다른 view와 함께 표시될 수 있습니다.

컨테이너 뷰 컨트롤러 하위 클래스는 해당 하위 클래스를 연결할 공개 인터페이스를 선언해야 합니다. 이러한 메서드의 특성은 개발자에게 달려 있으며, 생성하는 컨테이너의 시멘틱에 따라 달라집니다. 이에 따라 컨테이너에 하위 항목이 몇개나 표시되어야 할지, 언제 표시되어야 할지, 뷰 계층의 어느 위치에서 보여질지를 결정해야 합니다. view controller 클래스는 하위 view가 공유하는 관계를 정의합니다. 컨테이너에 대한 공개 인터페이스를 깔끔하게 설정하면 컨테이너의 동작 방법에 대한 비공개 구현 정보에 액세스하지 않고도 하위 컨트롤러가 논리적으로 기능을 사용할 수 있습니다.

하위 루트 뷰를 뷰 계층에 추가하기 전에 컨테이너 뷰 컨트롤러가 하위 뷰 컨트롤러를 연결해야 합니다. 이렇게 하면 iOS에서 이벤트를 하위 뷰 컨트롤러로 올바르게 라우팅하고 해당 컨트롤러가 관리하는 뷰를 볼 수 있습니다. 마찬가지로 하위 루트 뷰를 뷰 계층에서 제거한 후에는 해당 하위 뷰 컨트롤러의 연결을 끊어야 합니다. 이 연결을 만들거나 끊으려면 컨테이너가 기본 클래스에서 정의한 특정 메서드를 호출해야 합니다. 이러한 메서드는 컨테이너 클래스의 클라이언트가 호출하는 것이 아니라, 예상되는 containment 동작을 제공하기 위해 컨테이너의 구현에서만 사용됩니다.

자주 사용되는 필수 메서드들:

[addChildViewController(_:)](notion://www.notion.so/sagwa/etc/not-found)

[removeFromParentViewController()](notion://www.notion.so/sagwa/etc/not-found)

[willMove(toParentViewController:)](notion://www.notion.so/sagwa/etc/not-found)

[didMove(toParentViewController:)](notion://www.notion.so/sagwa/etc/not-found)

<aside>
❗ 알림

컨테이너 뷰 컨트롤러를 만들때 필수적으로 오버라이드 해야 할 메서드가 있는 것은 아닙니다.

기본적으로 회전 및 appearance 콜백은 자동적으로 하위 항목에 전달됩니다.
선택적으로 [whichAutomaticallyForwardRotationMethods()](notion://www.notion.so/sagwa/etc/not-found) 및 [automaticallyForwardAppearanceMethods](notion://www.notion.so/sagwa/etc/not-found) 메서드를 오버라이드하여 이 동작을 직접 제어할 수 있습니다.

</aside>

## 메모리 관리

메모리는 iOS에서 중요한 리소스이며, view controller는 중요한 시간에 메모리 공간을 줄일 수 있는 built-in 기능을 지원합니다. UIViewController 클래스는 불필요한 메모리를 해제하는 [didReceeMemoryWarning()](notion://www.notion.so/sagwa/etc/not-found) 메서드를 통해 낮은 메모리 상태를 자동으로 처리합니다.

## 상태 보존과 복원

view controller의 [restorationIdentifier](notion://www.notion.so/sagwa/etc/not-found)(복원 식별자) 속성에 값을 할당하면, 앱이 백그라운드로 전환될 때 시스템이 view controller에 인코딩을 요청할 수 있습니다. 요청에 따라 보존이 일어나는 경우 view controller는 restorationIdentifier가 있는 뷰 계층의 뷰를 보존합니다. view controller는 다른 상태를 자동으로 저장하지 않습니다. 커스텀 컨테이너 뷰 컨트롤러를 구현한다면 모든 하위 뷰 컨트롤러를 직접 인코딩해야 하고 인코딩될 각 하위 항목은 고유한 restorationIdentifier가 있어야 합니다.

시스템이 보존 또는 복원할 view controller를 결정하는 방법에 대한 자세한 내용은 [iOS용 앱 프로그래밍 가이드](notion://www.notion.so/sagwa/etc/not-found)를 참조하십시오.

## 쥬스메이커 STEP-3 예습

먼저 STEP-3에 필요한 내용을 정리했다.

1. App 내에서 ViewController끼리 데이터를 주고 받는 방법
2. Auto Layout

1번에는 여러가지 방법이 있지만 모델에 있는 데이터를 우리는 ViewController끼리 교환 해야 하기 때문에 Delegate 방식을 채택해서 진행하면 좋을 것 같다. 까지 생각해서 미리 적용 시켜보려 했지만! 역시 이해도 안하고 바로 써먹으려고 하다보니 절대안돼~ 주말에 공부하고 적용해보자.

# ****🔥 오늘의 3줄 회고****

- 1. 읽고 2. 이해하고 3. 사용하자
- 아직은 ViewController의 정확한 역할이 뭔지 모르겠다
- Delegate는 살살 덤벼줘 ;;