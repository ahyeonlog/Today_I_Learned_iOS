```swift
import UIKit

class CodeViewController: UIViewController {
    
    @IBOutlet weak var btn: UIButton!
    
    @IBOutlet weak var slider: UISlider!
    
    // code로 추가하는 액션
    func action() {
        
    }
    @objc func action(_ sender: Any) {
        print(#function)
    }
    func action(_ sender: Any, forEvent event: UIEvent) {
        
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let sel = #selector(action(_:))
        // for : event  종류
        btn.addTarget(self, action: sel, for: .touchUpInside)
    }
}

```
