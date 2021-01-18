# Keyframe Animation

```swift
    @IBOutlet weak var redView: UIView!
    
    func phase1() {
        let targetFrame = CGRect(x: view.center.x - 100, y: view.center.y - 100, width: 200, height: 200)
        redView.frame = targetFrame
    }
    
    func phase2() {
        redView.backgroundColor = UIColor.blue
    }
    
    func phase3() {
        let targetFrame = CGRect(x: 50, y: 100, width: 50, height: 50)
        redView.frame = targetFrame
        redView.backgroundColor = UIColor.red
    }
    
    
    @IBAction func animate(_ sender: Any) {
//        // 완료 블록을 활용해서 순차적으로 애니메이션 진행
//        // 중첩이 계속될 수 있음
//        UIView.animate(withDuration: 1, animations: {
//            self.phase1()
//        }, completion: { finished in
//            UIView.animate(withDuration: 1, animations: {
//                self.phase2()
//            }, completion: { finished in
//                UIView.animate(withDuration: 1, animations: {
//                    self.phase3()
//                })
//            })
//        })
        
        UIView.animateKeyframes(withDuration: 3, delay: 0, options: [], animations: {
            // withRelatvieStartTime: 전체애니메이션 시간에 대한 상대적인 값
            // relativeDuration: 실행시간
            UIView.addKeyframe(withRelativeStartTime: 0.0, relativeDuration: 0.3, animations: {
                self.phase1()
            })
            UIView.addKeyframe(withRelativeStartTime: 0.3, relativeDuration: 0.3, animations: {
                self.phase2()
            })
            UIView.addKeyframe(withRelativeStartTime: 0.6, relativeDuration: 0.4, animations: {
                self.phase3()
            })
        }, completion: nil)

    }
```
