# 220923_LinkedList

Date: 2022년 9월 23일

# ✏️ TIL (Today I Learned)

# 🔥 오늘의 목표

- [ ]  STEP-1 리팩토링
- [ ]  STEP-2 시작
- [ ]  

# 🔥 오늘 한 일

## STEP-1 Linked List로 수정하기

# ****🔥 공부한 내용****

queue를 단방향 LinkedList로 최소한의 기능만을 구현했다.

swift로는 처음 짜보는 개념이라 헷갈렸다. c++처럼 포인터를 쓰지 않고도 구현이 가능하다니

혹시라도 틀린 부분이나 조언해주실 부분있으시면 편하게 댓글 달아주세요!

```swift
class Node<T: CalculateItem> {
    let data: T
    var next: Node?
    
    init(data: T, next: Node? = nil) {
        self.data = data
        self.next = next
    }
}

struct CalculatorItemQueue<T: CalculateItem> {
    var head: Node<T>?
    var tail: Node<T>?
    var count = 0
    
    var isEmpty: Bool {
        return head == nil
    }
    
    mutating func enqueue(element: T) {
        let newNode: Node = Node(data: element)
        count += 1
        
        if isEmpty == true {
            head = newNode
            tail = newNode
            return
        } else {
            tail?.next = newNode
            tail = newNode
        }
    }
    
    mutating func dequeue() -> T? {
        if isEmpty == true {
            return nil
        }
        
        let data = head?.data
        head = head?.next
        count -= 1
        return data
    }
}
```

# ****🔥 문제점 → 해결 방법****

## Linked List에서 dequeue될때 원래 있던 head노드는 메모리에서 잘 해제 될까?

단순히 node에 deinit을 찍어보는 방식으로 확인해봤다. 물론 잘 해제 된다.

<aside>
✏️  클래스 인스턴스는 참조 카운트가 0이 되어야 메모리에서 사라진다.
head 에 새로운 노드를 가리켜 기존의 head가 가리키던 노드 인스턴스의 참조 카운트는 0이 된다.
그래서 메모리에서 사라지게 된다.

</aside>

# ****🔥 오늘의 3줄 회고****

- 몸 관리
- 멘탈 관리
- 눈 관리 👀