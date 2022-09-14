# 220914_Delgate_UILable

Date: 2022년 9월 14일

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  쥬스메이커에 Delegate 적용해보기
- [ ]  야곰닷넷 AutoLayout 공부
- [ ]  

# ****🔥 공부한 내용****

[****Anatomy of a Constraint****](https://www.notion.so/Anatomy-of-a-Constraint-e116d83fb1374e43adf28075b7834bff)

# ****🔥 문제점 → 해결 방법****

## UILable에 Layout을 초과하는 텍스트가 들어가게 되면 짤리는 현상

![Simulator Screen Shot - iPhone 14 Pro - 2022-09-14 at 20.58.16.png](220913_Delgate_UILable%20c0c92976187749e493af82c4ab0eb158/Simulator_Screen_Shot_-_iPhone_14_Pro_-_2022-09-14_at_20.58.16.png)

이럴 경우에는 UILabel의 사이즈를 조절해주는 메서드나 속성을 활용하면 된다.

```swift
func setAllLabelSizeToFit() {
        mutableStrawberryAmountLabel.sizeToFit()
        mutableBananaAmountLabel.sizeToFit()
        mutableKiwiAmountLabel.sizeToFit()
        mutablePineappleAmountLabel.sizeToFit()
        mutableMangoAmountLabel.sizeToFit()
}
```

나는 JuicieMaker 프로젝트에 `sizeToFit()` 을 활용해서 값이 업데이트 될 때마다 `setAllLabelSizeToFit()` 메서드를 호출해주는데 이건 추후에 AutoLayout 을 적용할때 조금 더 고민 해 볼 문제같다.

[[참고 블로그]](https://doorganizedcoding.tistory.com/entry/UILabel-size%EB%A5%BC-Text-size%EC%97%90-%EB%A7%9E%EC%B6%94%EB%8A%94-%EB%B0%A9%EB%B2%95%ED%98%B9%EC%9D%80-%EA%B7%B8-%EB%B0%98%EB%8C%80)
