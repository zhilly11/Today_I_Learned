# 220816_PairProgramming

Date: 2022년 8월 16일
Tag: Swift, iOS, 야곰

# ✏️ TIL (Today I Learned)

---

---

# ****🔥 학습 내용****

## 1. 짝 프로그래밍 (Pair Programming)

> 두 사람이 한 짝이 되어서 같이 프로그래밍을 한다.
> 

### 짝 프로그래밍의 효과?

1. 결함수가 적어진다! 
2. 통합 시간이 줄어든다!
3. 팀워크를 향상 시킨다!

### 짝 프로그래밍을 통해 어떤 것을 배울 수 있을까?

- Pair Debugging : 내가 생각도 못한 것을 옆 사람이 쉽게 찾을 수 있다.
- 발표자료 만들기, 전략짜기, 회의록 남기기 등 여러 작업이 가능하다.

### 규칙

1. 둘의 목표를 적는다.
2. 브레인 스토밍을 통해 목표에 맞게 task를 쪼갠다.
3. 어떤 식으로 접근할지, 어떤 task를 진행할지 정한다.
4. 15~20분 간격으로 드라이버와 네비게이터가 되어 진행한다.

### 역할

1. 드라이버
- 키보드를 잡은사람
- 독단적으로 코드 작성하지 않는다.
- 네비게이터 요청에만 움직인다.
- 드라이버는 네비게이터에게 자신의 의견을 말하거나 질문 할 수 없다.
1. 네비게이터
- 네비게이터는 명확하게 자신의 의사를 드라이버에게 요청한다.
- 세세한 것 하나까지 요청한다.
- 자신감 있게 요청한다.

### 첫 짝 프로그래밍 회고

- 아직 내가 알고있던 것들을 버리지 못했던 것 같다.
- 짝 프로그래밍 규칙을 완벽하게 지키긴 힘들었다…

## 2. 사전과제 설명하기

### 사전과제를 짝과 어떻게 구현했는지 상세하기 설명하고 서로 의견을 주고 받는 시간을 가졌다. 서로 아쉬웠던 점들을 얘기하고 피드백을 해봤다.

### 면담때 조언 받았던 부분 고치기

### 1. 강제 옵셔널 추출

사전과제때 알고리즘 문제 풀이에 익숙해서 이런식으로 옵셔널을 생각하지 않고 !를 마구마구 사용했다.

이제는 방법을 알았으니 다음부턴 꼭 활용하자

```swift
//Wrong
let greeting = readLine()!

//Correct
guard let greeting = readLine() else {
		print("잘못된 입력입니다.")
		break
}
```

### 2. Naming Convention

마찬가지로 Swift API Design Guidelines를 완벽하게 숙지하지 못해 Naming을 엉망진창으로 했었다..

날 잡고 블로그에 포스팅 해야겠다… 최대한 빠른 시일내로,,,,,,,

---

# ****🔥 문제점 / 고민한 점****

## 1. 어떻게 짝 프로그래밍을 진행해야할까

- 각각의 branch에서 작업을 해야할지 아니면 다른 방식으로 진행을 해야할지 고민했다.

## 2. 사전과제 설명 ,피드백

- 짝의 소스에서 문법적으로 모르는 부분들이 있어 정확한 피드백이 어려웠다.
- 나의 소스도 그새 기억나지 않는 부분들이 있어 설명이 버벅였던 것 같다.

---

# ****🔥 해결 방법****

## 1. 한 명의 fork된 Repository에서 Collaborator 기능을 사용하면 된다.

이런 방법을 사용하면 번갈아가면서 코딩이 가능하다!

## 2. 옵셔널과 클로져, 고차함수부분이 제일 헷갈리고 어려웠다.

오늘부터 정리를 시작해서 이번주 안에 블로그에 포스팅 해보자!

---