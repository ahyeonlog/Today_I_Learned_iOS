  ```swift
  
  class EventView: UIView {
   override func layoutMarginsDidChange() {
      super.layoutMarginsDidChange()
      
      if #available(iOS 11.0, *) {
         let target = directionalLayoutMargins
      } else {
         let target = layoutMargins
      }
   }
   
   @available(iOS 11.0, *)
   override func safeAreaInsetsDidChange() {
      super.safeAreaInsetsDidChange()
   }
}

class EventsViewController: UIViewController {
   @available(iOS 11.0, *)
   override func viewLayoutMarginsDidChange() {
      super.viewLayoutMarginsDidChange()
   }
   
   @available(iOS 11.0, *)
   override func viewSafeAreaInsetsDidChange() {
      super.viewSafeAreaInsetsDidChange()
   }
}

  ```
