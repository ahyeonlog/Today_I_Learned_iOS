# Property Animator

Property Animator는 UIView Animation을 대체하는 새로운 API이다. 최소 배포 버전이 iOS 10이라면 UIView Animation을 Property Animator로 대체해도 좋다.

```
Start, Pause, Resume, and Stop Animations
Cubic Bezier Timing Curve, Custom Timing Curve
Add Animation Blocks Dynamically
Interactive Animations
```

### Animation의 세가지 상태
[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbkFbSW5hY3RpdmVdIC0tPnxGaW5pc2h8IEJbQWN0aXZlXVxuQiAtLT58U3RvcHwgQ1tTdG9wcGVkXVxuQyAtLT58RmluaXNofCBBXG5CIC0tPnxTdGFydC9QYXVzZXwgQVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggVERcbkFbSW5hY3RpdmVdIC0tPnxGaW5pc2h8IEJbQWN0aXZlXVxuQiAtLT58U3RvcHwgQ1tTdG9wcGVkXVxuQyAtLT58RmluaXNofCBBXG5CIC0tPnxTdGFydC9QYXVzZXwgQVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

```swift

import UIKit

class PropertyAnimatorViewController: UIViewController {
    
    @IBOutlet weak var redView: UIView!
    
    var animator: UIViewPropertyAnimator?
    
    func moveAndResize() {
        let targetFrame = CGRect(x: view.center.x - 100, y: view.center.y - 100, width: 200, height: 200)
        redView.frame = targetFrame
    }
    
    @IBAction func reset(_ sender: Any?) {
        redView.backgroundColor = UIColor.red
        redView.frame = CGRect(x: 50, y: 100, width: 50, height: 50)
    }
    
    @IBAction func pause(_ sender: Any) {
        // animation을 일시 정지 : pauseAnimation
        // 이미 실행된 animation 비율은 fractionComplete로 확인
        animator?.pauseAnimation()
        print(animator?.fractionComplete)
    }
    
    @IBAction func animate(_ sender: Any) {
        // 메소드는 animator를 return
//        animator = UIViewPropertyAnimator.runningPropertyAnimator(withDuration: 7, delay: 0, options: [], animations: {
//            self.moveAndResize()
//        }, completion: { position in
//            switch position {
//            case .start:
//                print("Start")
//            case .end:
//                print("End")
//            case .current:
//                print("Current")
//            }
//
//        })
        // position: 애니메이션 종료 위치를 나타내는 열거형 전달
        
        
        // 생성자로 생성한 animator는 자동으로 실행되지 않는다.
        animator = UIViewPropertyAnimator(duration: 7, curve: .linear, animations: {
            self.moveAndResize()
        })
        animator?.addCompletion({ (position) in
            print(position)
        })
    }
    
    @IBAction func resume(_ sender: Any) {
        animator?.startAnimation()
    }
    
    @IBAction func stop(_ sender: Any) {
        // true: 별도 작업 없이 inactive상태로 전환
        // false: stop 상태로 전환 보통 finishAnimation()를 이어서 호출
        animator?.stopAnimation(false)
        animator?.finishAnimation(at: .current)
    }
    
    @IBAction func add(_ sender: Any) {
        // 파라미터로 전달된 animation을 프로퍼티애니메이터가 관리하는 실행스택에 추가함
        // inactive나 active 상태에서 호출!
        // stop 상태에서 호출하면 크래쉬!
        animator?.addAnimations({
            self.redView.backgroundColor = UIColor.blue
        }, delayFactor: 0)
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
    }
}

```

출처
- [UIViewPropertyAnimator](https://developer.apple.com/documentation/uikit/uiviewpropertyanimator)
- [UIViewAnimating](https://developer.apple.com/documentation/uikit/uiviewanimating)
- [UIViewImplicitlyAnimating](https://developer.apple.com/documentation/uikit/uiviewimplicitlyanimating)
- [Property-Based Animations](https://developer.apple.com/documentation/uikit/animation_and_haptics/property-based_animations?changes=_2)
