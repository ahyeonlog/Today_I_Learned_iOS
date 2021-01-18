# 🤸🏻‍♀️UIView Animation

UIView 클래스는 애니메이션에 사용되는 api를 type method로 제공한다. 에니메이션 api는 Block-based API이다. 최종값을 블록안에 작성하면 UIKit이 현재값에서 최종값으로 전환하는 애니메이션을 실행한다.
UIView에서 아래와 같은 속성들이 애니메이션을 지원한다.
```
frame
bounds
center
transform
alpha
backgroundColor
```
[Debug > Slow Animations]로 시뮬레이터에서 애니메이션을 슬로우 모들 진행할 ㅅ 있ㄷ.

```swift  
    @IBAction func animate(_ sender: Any) {
        var frame = redView.frame
        frame.origin = view.center
        frame.size = CGSize(width: 100, height: 100)

        UIView.animate(withDuration: 3) {
            self.redView.frame = frame    
            self.redView.alpha = 0.5
            self.redView.backgroundColor = UIColor.blue
        } completion: { (finished) in
            UIView.animate(withDuration: 3) {
                self.reset(nil)
            }
        }  
    }
```
`completion` : animation이 정상적으로 완료되면 true, 아니면 false가 전달


# UIView Animation Option

```swift
    @IBAction func animate(_ sender: Any) {
        let animations: () -> () = {
            var frame = self.redView.frame
            frame.origin = self.view.center
            frame.size = CGSize(width: 100, height: 100)
            self.redView.frame = frame
            self.redView.alpha = 0.5
            self.redView.backgroundColor = UIColor.blue
        }
        
        // allowUserInteraction : 애니메이션 동안은 터치가 안먹는데 터치를 가능하게 하는 옵션
        // beginFromCurrentState : 실행중인 애니메이션을 중지하고 현재 애니메이션 바로 실행
        UIView.animate(withDuration: 1, delay: 0.0, options: [.curveLinear, .repeat, .autoreverse], animations: animations, completion: nil)
    }
```

```swift
    // UIView Animation은 개별 애니메이션 중지할 수 없음(iOS 4에서 나온 오래된 것)
    // ==> 프로퍼티 애니메이터를 사용
    @IBAction func stop(_ sender: Any) {
        redView.layer.removeAllAnimations()
        reset(nil)
    }
```


참고
- [UIView](https://developer.apple.com/documentation/uikit/uiview)
- [UIView.AnimationOptions](https://developer.apple.com/documentation/uikit/uiview/animationoptions)
