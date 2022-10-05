# 220930_ScrollView_NumberFormatter

Date: 2022년 9월 30일

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  계산기 STEP-3 PR 보내기!!!!!!!!!!!!!!!!!!!
- [ ]  
- [ ]  

# 🔥 오늘 한 일

## 계산기 STEP-3 PR 보냄 휴;

## 계산기 README도 작성

## 

# ****🔥 공부한 내용****

## StackView 코드로 만드는 법!

```swift
let operandLabel = UILabel()
        operandLabel.text = displayNumberLabel.text
        operandLabel.textColor = .white

        let operatorLabel = UILabel()
        operatorLabel.text = displaySignLabel.text
        operatorLabel.textColor = .white

        let stackView = UIStackView(arrangedSubviews: [operatorLabel, operandLabel])
        // 거리주는 옵션
        stackView.spacing = 8
        stackView.translatesAutoresizingMaskIntoConstraints = false

```

## ScrollView에 요소가 추가될 때 자동으로 아래스크롤 되게 하는 법!

```swift
let contentOffsetPoint: CGPoint = CGPoint(x: .zero, y: formulaScrollView.contentSize.height)
        formulaScrollView.setContentOffset(contentOffsetPoint, animated: false)

```

## numberFormatter 쓰는법

```swift
let numberFormatter: NumberFormatter = NumberFormatter()
let stringNumber: String = "12345"

numberFormatter.maximumFractionDigits = 16
numberFormatter.numberStyle = .decimal

let result: String = numberFormatter.string(from: stringNumber)

```

이런식으로 간략하게 쓸 수 있다.

# ****🔥 오늘의 3줄 회고****

- 오늘의 나야 잘했다.
- 업보 청산 완료..
- 할땐 하고 쉴땐 쉬고 할하쉬쉬