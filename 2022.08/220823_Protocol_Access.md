# 220823_Protocol_Access

Date: 2022년 8월 23일

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  STEP-1 PR 코멘트 답변달기
- [ ]  STEP-2 진행 시작하기

# 🔥 오늘 한 일

## STEP-1 PR 코멘트 답변달기

## STEP-2 Flow chart 작성

## 접근제어자 공부

## Protocol 공부

# ****🔥 공부한 내용****

## 

# 접근 제어

접근제어란? 다른 소스 파일과 모듈에서 코드의 부분에 접근에 대해 제한한다!
즉, 코드의 구현 세부를 숨기고 해당 코드에 접근하고 사용될 수 있는 인터페이스를 지정할 수 있다!

특정 접근 수준을 클래스, 구조체, 열거형, 프로퍼티, 메서드, 초기화 구문, 서브스크립트에 할당 가능
Swift는 일반적인 시나리오에 대한 접근 수준을 명시적으로 제공해 접근제어 수준을 지정할 필요를 줄여 준다.
실제로 단일앱 작성시 접근제어 수준을 전혀 지정할 필요가 없다??

## 모듈과 소스 파일

Swift의 접근 제어 모델은 모듈과 소스 파일의 개념을 기초로 한다.

Xcode에서 각 빌드 타겟은 Swift에서 별도의 모듈로 처리된다.
여러 앺에서 해당 코드를 캡슐화 하고 재샤용 하기위해 앱의 코드의 여러 측면을 독립형 프레임워크로 그룹화 하면 해당 프레임워크 내에서 정의 한 모든 것은 앱 내에서 가져와서 사용되거나 다른 프레임워크 내에서 사용될 때 별도의 모듈에 속하게 된다.

## 접근 수준

Swift는 5개의 접근 수준 제공한다.

⬇️아래로 갈 수록 높은 제약의 접근 수준

- `Open`, `public` : 정의한 모듈의 모든 소스파일, import한 다른 모듈 소스파일에서 사용가능
- `internal` : 정의한 모듈의 모든 소스파일에선 사용 가능하지만, 외부 소스파일에선 사용 불가
- `File-private` : 자체 정의한 소스파일로 사용 제한, 세부 내용은 파일 전체에서 사용되고 기능의 특정 부분의 구현 세부정도를 가리기 위해 사용한다.
- `Private` : 둘러싸인 선언과 같은 파일에 있는 해당 선언의 확장으로 사용 제한, 세부 내용은 단일 선언 내에서만 사용되고 기능의 특정 부분의 구현 세부정보를 가리기 위해 사용

여기 까지 읽으면 어떨 때 어떤 접근 제어자를 사용해야할지 감이 안온다..

## 접근 수준의 기본 원칙

Swift에서 접근 수준은 기본 원칙을 따른다! : ***엔티티는 더 낮은 (더 제한적) 접근 수준을 가진 다른 엔티티로 정의할 수 없습니다.***

예를 들어:
* public 변수는 internal, file-private, 또는 private 타입으로 정의될 수 없습니다. public 변수는 어디서나 사용될 수 있지만 이 타입은 그렇지 못하기 때문입니다.
- 함수는 주변 코드에서 구성 타입을 사용할 수 없는 상황에서 함수를 사용할 수 있기 때문에 파라미터 타입과 반환 타입보다 더 높은 접근 수준을 가질 수 없습니다.

## 기본 접근 수준

몇가지 특정 예외를 포함하여 모든 엔티티는 명시적으로 접근 수준을 지정하지 않으면 internal의 기본 접근수준을 가진다.

## 접근 제어 구문

그렇다면 어떻게 작성할까?

```
public class SomePublicClass {}
internal class SomeInternalClass {}
fileprivate class SomeFilePrivateClass {}
private class SomePrivateClass {}

public var somePublicVariable = 0
internal let someInternalConstant = 0
fileprivate func someFilePrivateFunction() {}
private func somePrivateFunction() {}

```

## 서브 클래싱 (Subclassing)

하위 클래스는 상위 클래스의 접근 수준보다 높은 접근 수준을 가질 수 없다!
예를 들면 internal 상위 클래스에 public 하위 클래스를 작성할 수 없다.

또한 같은 모듈에 정의된 클래스의 경우 특정 접근 컨텍스트에 표시되는 경우 모든 클래스 멤버를 재 정의할 수 있다.
다른 모듈에 정의된 클래스의 경우 모든 open 클래스 멤버를 재 정의할 수 있다.

## <br>

---

# Protocol

#블로그

프로토콜은 메서드, 프로퍼티, 그리고 특정 작업이나 기능의 부분이 적합한 다른 요구사항의 청사진이다.
프로토콜은 요구사항의 구현을 제공하기 위해 클래스, 구조체, 열거형에 채택될 수 있다.
프로토콜의 요구사항에 충족하는 모든 타입은 프로토콜에 준수 한다고 한다.
준수하는 타입의 요구사항을 지정하는 것 외에도 일부를 구현하거나 준수하는 타입에 추가 기능을 구현하기 위해 프로토콜을 확장 할 수 있다.

## 프로토콜 구문

1. 클래스, 구조체, 그리고 열거형은 유사한 방법으로 프로토콜을 정의한다.

```
protocol SomeProtocol {
    // protocol definition goes here
}

```

1. 채택 : 타입의 이름 뒤에 프로토콜의 이름을 적어서 채택한다. 여러 프로토콜은 콤마로 목록화 한다.

```
struct SomeStructure: FirstProtocol, AnotherProtocol {
    // structure definition goes here
}

```

1. 상위 클래스를 가진 경우는 프로토콜의 이름을 적기전에 먼저 위치 시킨다.

```
class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
    // class definition goes here
}

```

## 프로퍼티 요구사항

프로퍼티는 특정 이름과 타입을 가진 인스턴스 프로퍼티 또는 타입 프로퍼티를 제공하기위해 준수하는 모든 타입을 요구할 수 있다.
프로토콜은 요구뒨 프로퍼티 이름과 타입만 지정하고 저장되거나 계산된 프로퍼티인지 지정하지 않는다.
그래서 프로토콜은 각 프로퍼티가 gettable 인지 settable 인지 지정해줘야 한다.

프로퍼티 요구사항은 항상 var 키워드와 함께 변수 프로퍼티로 선언 된다.

```
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}

```

## 

# ****🔥 오늘의 3줄 회고****

- Protocol 어려워
- 접근제어자 헷갈려
- 오늘은 진짜 진짜 일찍 자자