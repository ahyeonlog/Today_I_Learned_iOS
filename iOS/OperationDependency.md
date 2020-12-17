```swift
let backgroundQueue = OperationQueue()
let mainQueue = OperationQueue.main

var uiOperations = [Operation]()
var backgroundOperations = [Operation]()
```

```swift

@IBAction func startOperation(_ sender: Any) {
    uiOperations.removeAll()
    backgroundOperations.removeAll()
    
    DispatchQueue.global().async {
        let operation1 = CustomOperation1()
        self.uiOperations.append(operation)
        
        let operation2 = CustomOperation2()
        operation1.addDependency(operation2)
        self.backgroundOperations.append(operation2)
    
        self.backgroundQueue.addOperations(self.backgroundOperations, waitUntilFinished: false)
        // true > 완료될 때 까지 리턴하지 않음 mainQueue에서 사용하면 블로킹 가능성 생김!!
        self.mainQueue.addOperations(self.uiOperations, waitUntilFinished:  false)
    }
    
}
```

```swift
@IBAction func cancelOperation(_ sender: Any) {
    mainQueue.cancelAllOperations()
    uiOperations.forEach { ($0).cancel() }
    backgroundQueue.cancelAllOperations()
}
```
