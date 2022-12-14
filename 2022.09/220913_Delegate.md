# 220913_Delegate

Date: 2022년 9월 13일

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  Delegate 예제 만들어보기
- [ ]  
- [ ]  

# 🔥 오늘 한 일

## 학습활동

프로토콜이란?

- 내 수행원이 나 대신 처리해주는 일 : 총기 구매, 탄약 관리, 정보 수집
- 내 수행원이 갖춰야 하는 능력 : 총기사용자격증, 도청 자격증, 뛰어난 관찰력, 글로벌한 인맥

## Delegate 만들어보기

ViewController 간에 데이터를 주고 받을 수 있는 방법 중 하나이다.

Delegate는 프로그램의 한 개체가 다른 개체를 대신하거나 다른 개체와 연계하여 작동하는 단순하고 강력한 패턴이다. Delegate 개체는 다른 위임자에 대한 참조를 유지하고 적절한 시간에 해당 개체로 메시지를 보냅니다. 메시지는 위임 개체가 처리하려고 하거나 방금 처리한 이벤트를 위임자에게 알립니다. 위임자는 자신의 외관이나 응용 프로그램 내의 다른 오브젝트 상태를 갱신함으로써 메시지에 응답할 수 있습니다. 경우에 따라서는 임박한 이벤트 처리 방법에 영향을 주는 값을 반환할 수도 있습니다. 위임의 주요 가치는 하나의 중앙 개체에서 여러 개체의 동작을 쉽게 사용자 정의할 수 있다는 것이다.

## 실행 화면

[Simulator Screen Recording - iPhone 14 Pro - 2022-09-13 at 23.41.15.mp4](220913_Delegate%2038b7696d8547405fb58b278766a90a27/Simulator_Screen_Recording_-_iPhone_14_Pro_-_2022-09-13_at_23.41.15.mp4)

## 화면 구성(Storyboard)

 

![Untitled](220913_Delegate%2038b7696d8547405fb58b278766a90a27/Untitled.png)

먼저 구조를 혼자 이해한대로 그려봤습니다..

![Untitled](220913_Delegate%2038b7696d8547405fb58b278766a90a27/Untitled%201.png)

[참고 블로그](https://taekki-dev.tistory.com/36)

# ****🔥 오늘의 3줄 회고****

- 암기말고 이해하기
- 예제를 한 번 만들어보자
- 멘탈 관리 몸 관리