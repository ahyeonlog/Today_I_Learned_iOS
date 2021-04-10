```swift

import UIKit

class UserDefaultsViewController: UIViewController {
    
    @IBOutlet weak var keyLabel: UILabel!
    
    @IBOutlet weak var valueLabel: UILabel!
    
    @IBOutlet weak var lastUpdatedLabel: UILabel!
    
    func updateDateLabel() {
        let formatter = DateFormatter()
        formatter.dateStyle = .none
        formatter.timeStyle = .medium
        
        lastUpdatedLabel.text = formatter.string(from: Date())
    }
    
    let key = "sampleKey"
    
    @IBAction func saveData(_ sender: Any) {
        //    UserDefaults.standard.set("Hello", forKey: key)
        UserDefaults.standard.set(12.34, forKey: key)
    }
    
    @IBAction func loadData(_ sender: Any) {
        //    valueLabel.text = UserDefaults.standard.string(forKey: key) ?? "Not set"
        //    keyLabel.text = key
        
//        valueLabel.text = "\(UserDefaults.standard.integer(forKey: key))"
//        keyLabel.text = key
        valueLabel.text = "\(UserDefaults.standard.integer(forKey: thresholdKey))"
        keyLabel.text = thresholdKey
    }
    
    
    var token: NSObjectProtocol?
    
    deinit {
        if let token = token {
            NotificationCenter.default.removeObserver(token)
        }
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        token = NotificationCenter.default.addObserver(forName: UserDefaults.didChangeNotification, object: nil, queue: OperationQueue.main, using: { [weak self] (noti) in
            self?.updateDateLabel()
        })
        
        //print(UserDefaults.standard.dictionaryRepresentation())// 주로 디버깅 용도로 활용
//        print(UserDefaults.standard.dictionaryWithValues(forKeys: [key])) // 내가 저장한 요소만 출력
        
//        UserDefaults.standard.set(nil, forKey: key)
//        UserDefaults.standard.removeObject(forKey: key)
        
        
    }
}

```
