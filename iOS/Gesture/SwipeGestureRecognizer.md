
## GestureRecognizer 등록
```swift
override func viewDidLoad() {
    super.viewDidLoad()
        
    let leftSwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: #selector(handleSwipes(_:)))
    let rightSwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: #selector(handleSwipes(_:)))
        
    leftSwipeGestureRecognizer.direction = .left
    rightSwipeGestureRecognizer.direction = .right

    view.addGestureRecognizer(leftSwipeGestureRecognizer)
    view.addGestureRecognizer(rightSwipeGestureRecognizer)
}
```
## 동작 구현
```swift
@objc func handleSwipes(_ sender:UISwipeGestureRecognizer) {
    if (sender.direction == .left) {
        NSLog("Swipe Left")
    }
        
    if (sender.direction == .right) {
        NSLog("Swipe Right")
    }
}
```

## IBAction
```swift
@IBAction func handleSwipeGesture(_ sender: UISwipeGestureRecognizer) {
    if sender.state == .ended {
        dismiss(animated: true, completion: nil)
    }
}
```
