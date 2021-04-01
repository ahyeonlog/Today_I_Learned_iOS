```swift

// 백그라운드에서 작동하는 오퍼레이션 큐 생성
let queue = OperationQueue()
var isCancelled = false

@IBAction func startOperation(_ sender: Any) {
    isCancelled = false
    // 큐에 개별 오퍼레이션을 블록 형태로 추가
    queue.addOperation {
        autoreleasepool {
            for _ in 1..<100 {
                guard !self.isCancelled else {
                    return
                }
                print("◾️", separator: " ", terminator: " ")
                Thread.sleep(forTimeInterval: 0.3)
            }
        }
        
    }
    // 블록오퍼레이션을 생성하고 큐에 추가
    let op = BlockOperation {
        autoreleasepool {
            for _ in 1..<100 {
                guard !self.isCancelled else {
                    return
                }
                print("❣️", separator: " ", terminator: " ")
                Thread.sleep(forTimeInterval: 0.6)
            }
        }
    }
    queue.addOperation(op)
    
    // 블록오퍼레이션의 장점은 하나 이상의 블록을 추가할 수 있다는 점
    op.addExecutionBlock {
        autoreleasepool {
            for _ in 1..<100 {
                guard !self.isCancelled else {
                    return
                }
                print("💝", separator: " ", terminator: " ")
                Thread.sleep(forTimeInterval: 0.5)
            }
        }
    }
    
    
    
    let op2 = CustomOperation(type: "💮")
    queue.addOperation(op2)
    
    // 오퍼레이션에 구현된 작업이 완료된 후 호출됨
    op.completionBlock = {
        print("Done")
    }
}


@IBAction func cancelOperation(_ sender: Any) {
    isCancelled = true
    // 오퍼레이션큐의 모든 오퍼레이션을 취소
    queue.cancelAllOperations()
}

deinit {
    print(self, #function)
}
```

### 커스텀 오퍼레이션
> 커스텀 오퍼레이션은 main을 오버라이드하는게 포인트!
```swift
class CustomOperation: Operation {
    let type: String
    
    init(type: String) {
        self.type = type
    }
    override func main() {
        autoreleasepool {
            for _ in 1..<100 {
                guard !self.isCancelled else {
                    return
                }
                print(type, separator: " ", terminator: " ")
                Thread.sleep(forTimeInterval: 0.9)
            }
        }
    }
}
```

```swift
let op = CustomOperation(type: "💮")
OperationQueue.addOperation(op2)
```
