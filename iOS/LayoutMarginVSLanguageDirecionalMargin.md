```swift
class LayoutMarginsViewController: UIViewController {
   
   @IBOutlet weak var redView: UIView!
   
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      if #available(iOS 11.0, *) {
         navigationItem.largeTitleDisplayMode = .never
      }
   }

   
   override func viewDidLayoutSubviews() {
      super.viewDidLayoutSubviews()
      
      print("=== view.layoutMargins")
      print(view.layoutMargins)
      
      print("=== redView.layoutMargins")
      print(redView.layoutMargins)
   }
   
   
   func setupMargins() {
      if #available(iOS 11.0, *) {
         redView.directionalLayoutMargins = NSDirectionalEdgeInsets(top: 30, leading: 30, bottom: 30, trailing: 30)
      } else {
         redView.layoutMargins = UIEdgeInsets(top: 30, left: 30, bottom: 30, right: 30)
      }
   }
}

```
