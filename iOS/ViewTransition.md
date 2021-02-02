```swift


import UIKit

class ViewTransitionViewController: UIViewController {
    
    @IBOutlet weak var containerView: UIView!
    @IBOutlet weak var redView: UIView!
    @IBOutlet weak var blueView: UIView!
    
    @IBAction func startTransition(_ sender: Any) {
        
        // with 뒤에 transition이 실행될 컨테이너
        // animation block에서는 실제 트랜지션 구현
//        UIView.transition(with: containerView, duration: 1, options: [.transitionCurlUp], animations: {
//            self.redView.isHidden = !self.redView.isHidden
//            self.blueView.isHidden = !self.blueView.isHidden
//
//        }, completion: nil)
        
        
        // from to 동일한 컨테이너에 있어야 함
        UIView.transition(from: redView, to: blueView, duration: 1, options: [.transitionFlipFromLeft, .showHideTransitionViews], completion: {
            finished in UIView.transition(from: self.blueView, to: self.redView, duration: 1, options: [.transitionFlipFromRight, .showHideTransitionViews], completion: nil)
        })
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        blueView.isHidden = false
    }
}


```
