# Auto Layout Animation

```swift
    @IBOutlet weak var widthConstraint: NSLayoutConstraint!
    
    @IBOutlet weak var heightConstraint: NSLayoutConstraint!
    
    @IBAction func animate(_ sender: Any) {
        self.widthConstraint.constant = 200
        self.heightConstraint.constant = 200
        
        // 간혹 제약이 업데이트 안될경우에 사용
        redView.setNeedsUpdateConstraints()
        
        UIView.animate(withDuration: 0.3) {
            self.view.layoutIfNeeded()
        }
    }
```
제약은 UIView.animate() 바깥에 변경해야 한다.
