```swift
class FillParentViewController: UIViewController {
   
   @IBOutlet weak var bottomContainer: UIView!
   
   @IBOutlet weak var blueView: UIView!
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      layoutWithInitializer()
      //layoutWithVisualFormatLanguage()
      //layoutWithAnchor()
   }
}


extension FillParentViewController {
   func layoutWithInitializer() {
      blueView.translatesAutoresizingMaskIntoConstraints = false
      
      let leading = NSLayoutConstraint(item: blueView, attribute: .leading, relatedBy: .equal, toItem: bottomContainer, attribute: .leading, multiplier: 1.0, constant: 0)
      let top = NSLayoutConstraint(item: blueView, attribute: .top, relatedBy: .equal, toItem: bottomContainer, attribute: .top, multiplier: 1.0, constant: 0)
      let trailing = NSLayoutConstraint(item: blueView, attribute: .trailing, relatedBy: .equal, toItem: bottomContainer, attribute: .trailing, multiplier: 1.0, constant: 0)
      let bottom = NSLayoutConstraint(item: blueView, attribute: .bottom, relatedBy: .equal, toItem: bottomContainer, attribute: .bottom, multiplier: 1.0, constant: 0)
      
      NSLayoutConstraint.activate([leading, top, trailing, bottom])
   }
}

extension FillParentViewController {
   func layoutWithVisualFormatLanguage() {
      blueView.translatesAutoresizingMaskIntoConstraints = false
      
      let horzFmt = "|[b]|"
      let vertFmt = "V:|[b]|"
      
      let views: [String: Any] = ["b": blueView]
      
      let horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt, options: [], metrics: nil, views: views)
      let vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt, options: [], metrics: nil, views: views)
      
      NSLayoutConstraint.activate(horzConstraints + vertConstraints)
   }
}



extension FillParentViewController {
   func layoutWithAnchor() {
      blueView.translatesAutoresizingMaskIntoConstraints = false
      
      blueView.leadingAnchor.constraint(equalTo: bottomContainer.leadingAnchor).isActive = true
      blueView.topAnchor.constraint(equalTo: bottomContainer.topAnchor).isActive = true
      blueView.trailingAnchor.constraint(equalTo: bottomContainer.trailingAnchor).isActive = true
      blueView.bottomAnchor.constraint(equalTo: bottomContainer.bottomAnchor).isActive = true
   }
}

```

```swift
class FixedFrameViewController: UIViewController {
   
   @IBOutlet weak var redView: UIView!
   
   @IBOutlet weak var blueView: UIView!
   
   @IBOutlet weak var bottomContainer: UIView!
   
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      layoutWithInitializer()
      //layoutWithVisualFormatLanguage()
      //layoutWithAnchor()
   }
}

extension FixedFrameViewController {
   func layoutWithInitializer() {
      redView.translatesAutoresizingMaskIntoConstraints = false
      blueView.translatesAutoresizingMaskIntoConstraints = false
      // 슈퍼뷰의 마진을 기준으로 하기 때문에 topMargin
      let leading = NSLayoutConstraint(item: redView, attribute: .leading, relatedBy: .equal, toItem: bottomContainer, attribute: .leadingMargin, multiplier: 1.0, constant: 0)
      let top = NSLayoutConstraint(item: redView, attribute: .top, relatedBy: .equal, toItem: bottomContainer, attribute: .topMargin, multiplier: 1.0, constant: 0)
      var width = NSLayoutConstraint(item: redView, attribute: .width, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
      var height = NSLayoutConstraint(item: redView, attribute: .height, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
      
      NSLayoutConstraint.activate([leading, top, width, height])
    // 슈퍼 뷰의 마진이 아니라 슈퍼 뷰를 기준
      let trailing = NSLayoutConstraint(item: blueView, attribute: .trailing, relatedBy: .equal, toItem: bottomContainer, attribute: .trailing, multiplier: 1.0, constant: -20)
      let bottom = NSLayoutConstraint(item: blueView, attribute: .bottom, relatedBy: .equal, toItem: bottomContainer, attribute: .bottom, multiplier: 1.0, constant: -20)
    // toItem 없을 땐 nil 전달
      width = NSLayoutConstraint(item: blueView, attribute: .width, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
      height = NSLayoutConstraint(item: blueView, attribute: .height, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
      
      NSLayoutConstraint.activate([trailing, bottom, width, height])
   }
}

extension FixedFrameViewController {
   func layoutWithVisualFormatLanguage() {
      redView.translatesAutoresizingMaskIntoConstraints = false
      blueView.translatesAutoresizingMaskIntoConstraints = false
      // - : superview의 마진
     // 원래 ==100 이지만 equql의 겨우 == 생략 가능
      var horzFmt = "|-[red(100)]"
      var vertFmt = "V:|-[red(100)]"
      
      let views: [String: Any] = ["red": redView, "blue": blueView]
      
      var horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt, options: [], metrics: nil, views: views)
      var vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt, options: [], metrics: nil, views: views)
      
      NSLayoutConstraint.activate(horzConstraints + vertConstraints)
      
      horzFmt = "[blue(100)]-20-|"
      vertFmt = "V:[blue(100)]-20-|"
      
      horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt, options: [], metrics: nil, views: views)
      vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt, options: [], metrics: nil, views: views)
      NSLayoutConstraint.activate(horzConstraints + vertConstraints)
   }
}

extension FixedFrameViewController {
   func layoutWithAnchor() {
      redView.translatesAutoresizingMaskIntoConstraints = false
      blueView.translatesAutoresizingMaskIntoConstraints = false
      
      bottomContainer.layoutMarginsGuide.leadingAnchor.constraint(equalTo: redView.leadingAnchor).isActive = true
      bottomContainer.layoutMarginsGuide.topAnchor.constraint(equalTo: redView.topAnchor).isActive = true
      redView.widthAnchor.constraint(equalToConstant: 100).isActive = true
      redView.heightAnchor.constraint(equalToConstant: 100).isActive = true
      
      bottomContainer.trailingAnchor.constraint(equalTo: blueView.trailingAnchor, constant: 20).isActive = true
      blueView.bottomAnchor.constraint(equalTo: bottomContainer.bottomAnchor, constant: -20).isActive = true
      blueView.widthAnchor.constraint(equalToConstant: 100).isActive = true
      blueView.heightAnchor.constraint(equalToConstant: 100).isActive = true
   }
}
```
```swift
class CustomHeaderViewController: UIViewController {
   
   @IBOutlet weak var blueView: UIView!
   
   
   @IBAction func updateTopConstraint(_ sender: UISwitch) {
      
      
      if sender.isOn {
         topToSuperview?.isActive = false
         topToSafeArea?.isActive = true
      } else {
         topToSafeArea?.isActive = false
         topToSuperview?.isActive = true
      }
   }
   
   var topToSuperview: NSLayoutConstraint?
   var topToSafeArea: NSLayoutConstraint?
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      layoutWithInitializer()
      //layoutWithVisualFormatLanguage()
      //layoutWithAnchor()
   }
}

extension CustomHeaderViewController {
   func layoutWithInitializer() {
      blueView.translatesAutoresizingMaskIntoConstraints = false
      
      let leading = NSLayoutConstraint(item: blueView, attribute: .leading, relatedBy: .equal, toItem: view, attribute: .leading, multiplier: 1.0, constant: 0.0)
      let top = NSLayoutConstraint(item: blueView, attribute: .top, relatedBy: .equal, toItem: view, attribute: .top, multiplier: 1.0, constant: 0.0)
      let trailing = NSLayoutConstraint(item: blueView, attribute: .trailing, relatedBy: .equal, toItem: view, attribute: .trailing, multiplier: 1.0, constant: 0.0)
      let height = NSLayoutConstraint(item: blueView, attribute: .height, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
      NSLayoutConstraint.activate([leading, top, trailing, height])
      
      topToSuperview = top
      
      if #available(iOS 11.0, *) {
         topToSafeArea = NSLayoutConstraint(item: blueView, attribute: .top, relatedBy: .equal, toItem: view.safeAreaLayoutGuide, attribute: .top, multiplier: 1.0, constant: 0.0)
      } else {
         topToSafeArea = NSLayoutConstraint(item: blueView, attribute: .top, relatedBy: .equal, toItem: topLayoutGuide, attribute: .bottom, multiplier: 1.0, constant: 0.0)
      }
   }
}

extension CustomHeaderViewController {
   func layoutWithVisualFormatLanguage() {
      blueView.translatesAutoresizingMaskIntoConstraints = false
      
      let horzFmt = "|[blue]|"
      let vertFmt = "V:|[blue(100)]"
      
      let views: [String: Any] = ["blue": blueView]
      
      let horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt, options: [], metrics: nil, views: views)
      let vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt, options: [], metrics: nil, views: views)
      NSLayoutConstraint.activate(horzConstraints + vertConstraints)
   }
}

extension CustomHeaderViewController {
   func layoutWithAnchor() {
     blueView.translatesAutoresizingMaskIntoConstraints = false
      
      blueView.leadingAnchor.constraint(equalTo: view.leadingAnchor).isActive = true
      blueView.trailingAnchor.constraint(equalTo: view.trailingAnchor).isActive = true
      blueView.heightAnchor.constraint(equalToConstant: 100).isActive = true
      
      topToSuperview = blueView.topAnchor.constraint(equalTo: view.topAnchor)
      topToSuperview?.isActive = true
      
      if #available(iOS 11.0, *) {
         topToSafeArea = blueView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor)
      } else {
         topToSafeArea = blueView.topAnchor.constraint(equalTo: topLayoutGuide.bottomAnchor)
      }
   }
}

```

```swift
class GridViewController: UIViewController {
   
   @IBOutlet weak var redView: UIView!
   @IBOutlet weak var blueView: UIView!
   @IBOutlet weak var yellowView: UIView!
   @IBOutlet weak var blackView: UIView!
   
   @IBOutlet weak var bottomContainer: UIView!
   
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      //layoutWithInitializer()
      //layoutWithVisualFormatLanguage()
      layoutWithAnchor()
   }
}



extension GridViewController {
   func layoutWithInitializer() {
      redView.translatesAutoresizingMaskIntoConstraints = false
      blueView.translatesAutoresizingMaskIntoConstraints = false
      yellowView.translatesAutoresizingMaskIntoConstraints = false
      blackView.translatesAutoresizingMaskIntoConstraints = false
      
      let margin: CGFloat = 10.0
      
      var leading = NSLayoutConstraint(item: redView, attribute: .leading, relatedBy: .equal, toItem: bottomContainer, attribute: .leading, multiplier: 1.0, constant: margin)
      var top = NSLayoutConstraint(item: redView, attribute: .top, relatedBy: .equal, toItem: bottomContainer, attribute: .top, multiplier: 1.0, constant: margin)
      var trailing = NSLayoutConstraint(item: redView, attribute: .trailing, relatedBy: .equal, toItem: blueView, attribute: .leading, multiplier: 1.0, constant: -margin)
      var bottom = NSLayoutConstraint(item: redView, attribute: .bottom, relatedBy: .equal, toItem: yellowView, attribute: .top, multiplier: 1.0, constant: -margin)
      NSLayoutConstraint.activate([leading, top, trailing, bottom])
      
      top = NSLayoutConstraint(item: blueView, attribute: .top, relatedBy: .equal, toItem: bottomContainer, attribute: .top, multiplier: 1.0, constant: margin)
      trailing = NSLayoutConstraint(item: blueView, attribute: .trailing, relatedBy: .equal, toItem: bottomContainer, attribute: .trailing, multiplier: 1.0, constant: -margin)
      bottom = NSLayoutConstraint(item: blueView, attribute: .bottom, relatedBy: .equal, toItem: blackView, attribute: .top, multiplier: 1.0, constant: -margin)
      NSLayoutConstraint.activate([top, trailing, bottom])
      
      leading = NSLayoutConstraint(item: yellowView, attribute: .leading, relatedBy: .equal, toItem: bottomContainer, attribute: .leading, multiplier: 1.0, constant: margin)
      bottom = NSLayoutConstraint(item: yellowView, attribute: .bottom, relatedBy: .equal, toItem: bottomContainer, attribute: .bottom, multiplier: 1.0, constant: -margin)
      trailing = NSLayoutConstraint(item: yellowView, attribute: .trailing, relatedBy: .equal, toItem: blackView, attribute: .leading, multiplier: 1.0, constant: -margin)
      NSLayoutConstraint.activate([leading, bottom, trailing])
      
      trailing = NSLayoutConstraint(item: blackView, attribute: .trailing, relatedBy: .equal, toItem: bottomContainer, attribute: .trailing, multiplier: 1.0, constant: -margin)
      bottom = NSLayoutConstraint(item: blackView, attribute: .bottom, relatedBy: .equal, toItem: bottomContainer, attribute: .bottom, multiplier: 1.0, constant: -margin)
      NSLayoutConstraint.activate([trailing, bottom])
      
      let list: [UIView] = [blueView, yellowView, blackView]
      for v in list {
         let equalWidth = NSLayoutConstraint(item: v, attribute: .width, relatedBy: .equal, toItem: redView, attribute: .width, multiplier: 1.0, constant: 0.0)
         let equalHeight = NSLayoutConstraint(item: v, attribute: .height, relatedBy: .equal, toItem: redView, attribute: .height, multiplier: 1.0, constant: 0.0)
         NSLayoutConstraint.activate([equalWidth, equalHeight])
      }
   }
}



extension GridViewController {
   func layoutWithVisualFormatLanguage() {
      redView.translatesAutoresizingMaskIntoConstraints = false
      blueView.translatesAutoresizingMaskIntoConstraints = false
      yellowView.translatesAutoresizingMaskIntoConstraints = false
      blackView.translatesAutoresizingMaskIntoConstraints = false
      
      let margin: CGFloat = 10.0
      
    // metric 으로 숫자를 대신할 수 있음
      //let horzFmt1 = "|-10-[redView]-10-[blueView]-10-|"
      let horzFmt1 = "|-m-[red]-m-[blue(==red)]-m-|"
      let horzFmt2 = "|-m-[yellow]-m-[black(==yellow)]-m-|"
      let vertFmt1 = "V:|-m-[red]-m-[yellow(==red)]-m-|"
      let vertFmt2 = "V:|-m-[blue]-m-[black(==blue)]-m-|"
      
      let views: [String: Any] = ["red": redView,
                                  "blue": blueView,
                                  "yellow": yellowView,
                                  "black": blackView]
      
      let metrics: [String: Any] = ["m": margin]
      
      var horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt1, options: [], metrics: metrics, views: views)
      NSLayoutConstraint.activate(horzConstraints)
      
      horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt2, options: [], metrics: metrics, views: views)
      NSLayoutConstraint.activate(horzConstraints)
      
      var vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt1, options: [], metrics: metrics, views: views)
      NSLayoutConstraint.activate(vertConstraints)
      
      vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt2, options: [], metrics: metrics, views: views)
      NSLayoutConstraint.activate(vertConstraints)
   }
}


extension GridViewController {
   func layoutWithAnchor() {
      redView.translatesAutoresizingMaskIntoConstraints = false
      blueView.translatesAutoresizingMaskIntoConstraints = false
      yellowView.translatesAutoresizingMaskIntoConstraints = false
      blackView.translatesAutoresizingMaskIntoConstraints = false
      
      let margin: CGFloat = 10.0
      
      redView.leadingAnchor.constraint(equalTo: bottomContainer.leadingAnchor, constant: margin).isActive = true
      redView.topAnchor.constraint(equalTo: bottomContainer.topAnchor, constant: margin).isActive = true
      redView.trailingAnchor.constraint(equalTo: blueView.leadingAnchor, constant: -margin).isActive = true
      redView.bottomAnchor.constraint(equalTo: yellowView.topAnchor, constant: -margin).isActive = true
      
      blueView.topAnchor.constraint(equalTo: bottomContainer.topAnchor, constant: margin).isActive = true
      blueView.trailingAnchor.constraint(equalTo: bottomContainer.trailingAnchor, constant: -margin).isActive = true
      blueView.bottomAnchor.constraint(equalTo: blackView.topAnchor, constant: -margin).isActive = true
      
      yellowView.leadingAnchor.constraint(equalTo: bottomContainer.leadingAnchor, constant: margin).isActive = true
      yellowView.trailingAnchor.constraint(equalTo: blackView.leadingAnchor, constant: -margin).isActive = true
      yellowView.bottomAnchor.constraint(equalTo: bottomContainer.bottomAnchor, constant: -margin).isActive = true
      
      blackView.trailingAnchor.constraint(equalTo: bottomContainer.trailingAnchor, constant: -margin).isActive = true
      blackView.bottomAnchor.constraint(equalTo: bottomContainer.bottomAnchor, constant: -margin).isActive = true
      
      blueView.widthAnchor.constraint(equalTo: redView.widthAnchor).isActive = true
      blueView.heightAnchor.constraint(equalTo: redView.heightAnchor).isActive = true
      yellowView.widthAnchor.constraint(equalTo: redView.widthAnchor).isActive = true
      yellowView.heightAnchor.constraint(equalTo: redView.heightAnchor).isActive = true
      blackView.widthAnchor.constraint(equalTo: redView.widthAnchor).isActive = true
      blackView.heightAnchor.constraint(equalTo: redView.heightAnchor).isActive = true
   }
}

```

```swift

class AlignCenterViewController: UIViewController {
   
   @IBOutlet weak var bottomContainer: UIView!
   
   @IBOutlet weak var titleLabel: UILabel!
   
   @IBOutlet weak var bottomLineView: UIView!
   
   
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      //layoutWithInitializer()
      //layoutWithVisualFormatLanguage()
      layoutWithAnchor()
   }
}

extension AlignCenterViewController {
   func layoutWithInitializer() {
      titleLabel.translatesAutoresizingMaskIntoConstraints = false
      bottomLineView.translatesAutoresizingMaskIntoConstraints = false
      
      var centerX = NSLayoutConstraint(item: titleLabel, attribute: .centerX, relatedBy: .equal, toItem: bottomContainer, attribute: .centerX, multiplier: 1.0, constant: 0.0)
      let centerY = NSLayoutConstraint(item: titleLabel, attribute: .centerY, relatedBy: .equal, toItem: bottomContainer, attribute: .centerY, multiplier: 1.0, constant: 0.0)
      
      NSLayoutConstraint.activate([centerX, centerY])
      
      centerX = NSLayoutConstraint(item: bottomLineView, attribute: .centerX, relatedBy: .equal, toItem: titleLabel, attribute: .centerX, multiplier: 1.0, constant: 0.0)
      let top = NSLayoutConstraint(item: bottomLineView, attribute: .top, relatedBy: .equal, toItem: titleLabel, attribute: .bottom, multiplier: 1.0, constant: 10)
      let width = NSLayoutConstraint(item: bottomLineView, attribute: .width, relatedBy: .equal, toItem: titleLabel, attribute: .width, multiplier: 1.0, constant: 0.0)
      let height = NSLayoutConstraint(item: bottomLineView, attribute: .height, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 5.0)
      
      NSLayoutConstraint.activate([centerX, top, width, height])
   }
}


extension AlignCenterViewController {
   func layoutWithVisualFormatLanguage() {
      titleLabel.translatesAutoresizingMaskIntoConstraints = false
      bottomLineView.translatesAutoresizingMaskIntoConstraints = false
      // VFL 로는 표현 못하는 것도 있음
      titleLabel.centerXAnchor.constraint(equalTo: bottomContainer.centerXAnchor).isActive = true
      titleLabel.centerYAnchor.constraint(equalTo: bottomContainer.centerYAnchor).isActive = true
      
      bottomLineView.widthAnchor.constraint(equalTo: titleLabel.widthAnchor).isActive = true
      
      let vertFmt = "V:[lbl]-10-[line(==5)]"
      let views: [String: Any] = ["lbl": titleLabel, "line": bottomLineView]
      
      let vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt, options: .alignAllCenterX, metrics: nil, views: views)
      NSLayoutConstraint.activate(vertConstraints)
      
      
   }
}

extension AlignCenterViewController {
   func layoutWithAnchor() {
      titleLabel.translatesAutoresizingMaskIntoConstraints = false
      bottomLineView.translatesAutoresizingMaskIntoConstraints = false
      
      titleLabel.centerXAnchor.constraint(equalTo: bottomContainer.centerXAnchor).isActive = true
      titleLabel.centerYAnchor.constraint(equalTo: bottomContainer.centerYAnchor).isActive = true
      
      bottomLineView.widthAnchor.constraint(equalTo: titleLabel.widthAnchor).isActive = true
      
      bottomLineView.topAnchor.constraint(equalTo: titleLabel.bottomAnchor, constant: 10).isActive = true
      bottomLineView.centerXAnchor.constraint(equalTo: titleLabel.centerXAnchor).isActive = true
      bottomLineView.heightAnchor.constraint(equalToConstant: 5).isActive = true
   }
}

```

```swift
class AlignEdgeViewController: UIViewController {
   
   @IBOutlet weak var topContainer: UIView!
   
   @IBOutlet weak var bottomContainer: UIView!
   
   @IBOutlet weak var nameTitleLabel: UILabel!
   
   @IBOutlet weak var nameInputField: UITextField!
   
   @IBOutlet weak var emailTitleLabel: UILabel!
   
   @IBOutlet weak var emailInputField: UITextField!
   
   @IBOutlet weak var confirmButton: UIButton!
   
   var anchorView: UIView {
      return nameTitleLabel
   }
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      if #available(iOS 11.0, *) {
         var current = topContainer.directionalLayoutMargins
         current.leading = 30
         
         topContainer.directionalLayoutMargins = current
         bottomContainer.directionalLayoutMargins = topContainer.directionalLayoutMargins
      } else {
         var current = topContainer.layoutMargins
         current.left = 30
         
         topContainer.layoutMargins = current
         bottomContainer.layoutMargins = topContainer.layoutMargins
      }
      
      //layoutWithInitializer()
      layoutWithVisualFormatLanguage()
      //layoutWithAnchor()
   }
}

extension AlignEdgeViewController {
   func layoutWithInitializer() {
      nameTitleLabel.translatesAutoresizingMaskIntoConstraints = false
      nameInputField.translatesAutoresizingMaskIntoConstraints = false
      emailTitleLabel.translatesAutoresizingMaskIntoConstraints = false
      emailInputField.translatesAutoresizingMaskIntoConstraints = false
      confirmButton.translatesAutoresizingMaskIntoConstraints = false
      
      var leading = NSLayoutConstraint(item: nameTitleLabel, attribute: .leading, relatedBy: .equal, toItem: bottomContainer, attribute: .leadingMargin, multiplier: 1.0, constant: 0)
      var top = NSLayoutConstraint(item: nameTitleLabel, attribute: .top, relatedBy: .equal, toItem: bottomContainer, attribute: .topMargin, multiplier: 1.0, constant: 0)
      var trailing = NSLayoutConstraint(item: nameTitleLabel, attribute: .trailing, relatedBy: .equal, toItem: bottomContainer, attribute: .trailingMargin, multiplier: 1.0, constant: 0)
      
      NSLayoutConstraint.activate([leading, top, trailing])
      
      top = NSLayoutConstraint(item: nameInputField, attribute: .top, relatedBy: .equal, toItem: nameTitleLabel, attribute: .bottom, multiplier: 1.0, constant: 10.0)
      leading = NSLayoutConstraint(item: nameInputField, attribute: .leading, relatedBy: .equal, toItem: anchorView, attribute: .leading, multiplier: 1.0, constant: 0.0)
      trailing = NSLayoutConstraint(item: nameInputField, attribute: .trailing, relatedBy: .equal, toItem: anchorView, attribute: .trailing, multiplier: 1.0, constant: 0.0)
      
      NSLayoutConstraint.activate([leading, top, trailing])
      
      top = NSLayoutConstraint(item: emailTitleLabel, attribute: .top, relatedBy: .equal, toItem: nameInputField, attribute: .bottom, multiplier: 1.0, constant: 20.0)
      leading = NSLayoutConstraint(item: emailTitleLabel, attribute: .leading, relatedBy: .equal, toItem: anchorView, attribute: .leading, multiplier: 1.0, constant: 0.0)
      trailing = NSLayoutConstraint(item: emailTitleLabel, attribute: .trailing, relatedBy: .equal, toItem: anchorView, attribute: .trailing, multiplier: 1.0, constant: 0.0)
      
      NSLayoutConstraint.activate([leading, top, trailing])
      
      top = NSLayoutConstraint(item: emailInputField, attribute: .top, relatedBy: .equal, toItem: emailTitleLabel, attribute: .bottom, multiplier: 1.0, constant: 10.0)
      leading = NSLayoutConstraint(item: emailInputField, attribute: .leading, relatedBy: .equal, toItem: anchorView, attribute: .leading, multiplier: 1.0, constant: 0.0)
      trailing = NSLayoutConstraint(item: emailInputField, attribute: .trailing, relatedBy: .equal, toItem: anchorView, attribute: .trailing, multiplier: 1.0, constant: 0.0)
      
      NSLayoutConstraint.activate([leading, top, trailing])
      
      leading = NSLayoutConstraint(item: confirmButton, attribute: .leading, relatedBy: .equal, toItem: anchorView, attribute: .leading, multiplier: 1.0, constant: 0.0)
      trailing = NSLayoutConstraint(item: confirmButton, attribute: .trailing, relatedBy: .equal, toItem: anchorView, attribute: .trailing, multiplier: 1.0, constant: 0.0)
      top = NSLayoutConstraint(item: confirmButton, attribute: .top, relatedBy: .greaterThanOrEqual, toItem: emailInputField, attribute: .bottom, multiplier: 1.0, constant: 10)
      let bottom = NSLayoutConstraint(item: confirmButton, attribute: .bottom, relatedBy: .equal, toItem: bottomContainer, attribute: .bottomMargin, multiplier: 1.0, constant: 0.0)
      let height = NSLayoutConstraint(item: confirmButton, attribute: .height, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 40.0)
      
      NSLayoutConstraint.activate([leading, trailing, top, bottom, height])
   }
}


extension AlignEdgeViewController {
   func layoutWithVisualFormatLanguage() {
      nameTitleLabel.translatesAutoresizingMaskIntoConstraints = false
      nameInputField.translatesAutoresizingMaskIntoConstraints = false
      emailTitleLabel.translatesAutoresizingMaskIntoConstraints = false
      emailInputField.translatesAutoresizingMaskIntoConstraints = false
      confirmButton.translatesAutoresizingMaskIntoConstraints = false
      
      let views: [String: Any] = ["nameTitle": nameTitleLabel, "nameInput": nameInputField, "emailTitle": emailTitleLabel, "emailInput": emailInputField, "btn": confirmButton]
      
      let horzFmt = "|-[nameTitle]-|"
      let horzConstraints = NSLayoutConstraint.constraints(withVisualFormat: horzFmt, options: [], metrics: nil, views: views)
      
      NSLayoutConstraint.activate(horzConstraints)
      
      let vertFmt = "V:|-[nameTitle]-10-[nameInput]-20-[emailTitle]-10-[emailInput]-(>=10)-[btn(40)]-|"
      let vertConstraints = NSLayoutConstraint.constraints(withVisualFormat: vertFmt, options: [.alignAllLeading, .alignAllTrailing], metrics: nil, views: views)
      
      NSLayoutConstraint.activate(vertConstraints)
   }
}


extension AlignEdgeViewController {
   func layoutWithAnchor() {
      nameTitleLabel.translatesAutoresizingMaskIntoConstraints = false
      nameInputField.translatesAutoresizingMaskIntoConstraints = false
      emailTitleLabel.translatesAutoresizingMaskIntoConstraints = false
      emailInputField.translatesAutoresizingMaskIntoConstraints = false
      confirmButton.translatesAutoresizingMaskIntoConstraints = false
      
      let margins = bottomContainer.layoutMarginsGuide
      
      nameTitleLabel.leadingAnchor.constraint(equalTo: margins.leadingAnchor).isActive = true
      nameTitleLabel.topAnchor.constraint(equalTo: margins.topAnchor).isActive = true
      nameTitleLabel.trailingAnchor.constraint(equalTo: margins.trailingAnchor).isActive = true
      
      nameInputField.leadingAnchor.constraint(equalTo: nameTitleLabel.leadingAnchor).isActive = true
      nameInputField.topAnchor.constraint(equalTo: nameTitleLabel.bottomAnchor, constant: 10).isActive = true
      nameInputField.trailingAnchor.constraint(equalTo: nameTitleLabel.trailingAnchor).isActive = true
      
      emailTitleLabel.leadingAnchor.constraint(equalTo: nameTitleLabel.leadingAnchor).isActive = true
      emailTitleLabel.topAnchor.constraint(equalTo: nameInputField.bottomAnchor, constant: 20).isActive = true
      emailTitleLabel.trailingAnchor.constraint(equalTo: nameTitleLabel.trailingAnchor).isActive = true
      
      emailInputField.leadingAnchor.constraint(equalTo: nameTitleLabel.leadingAnchor).isActive = true
      emailInputField.topAnchor.constraint(equalTo: emailTitleLabel.bottomAnchor, constant: 10).isActive = true
      emailInputField.trailingAnchor.constraint(equalTo: nameTitleLabel.trailingAnchor).isActive = true
      
      confirmButton.leadingAnchor.constraint(equalTo: nameTitleLabel.leadingAnchor).isActive = true
      confirmButton.topAnchor.constraint(greaterThanOrEqualTo: emailInputField.bottomAnchor, constant: 10).isActive = true
      confirmButton.trailingAnchor.constraint(equalTo: nameTitleLabel.trailingAnchor).isActive = true
      confirmButton.bottomAnchor.constraint(equalTo: margins.bottomAnchor).isActive = true
      confirmButton.heightAnchor.constraint(equalToConstant: 40).isActive = true
      
   }
}

```

```swift
class AnimationViewController: UIViewController {
   @IBOutlet weak var redView: UIView!
   
   @IBOutlet weak var widthConstraint: NSLayoutConstraint!
   
   @IBOutlet weak var heightConstraint: NSLayoutConstraint!
   
   @IBOutlet weak var centerXConstraint: NSLayoutConstraint!
   
   @IBOutlet weak var centerYConstraint: NSLayoutConstraint!
   
   
   @IBAction func animate(_ sender: Any) {
      widthConstraint.constant = CGFloat(arc4random_uniform(91)) + 10
      heightConstraint.constant = CGFloat(arc4random_uniform(91)) + 10
      
      centerXConstraint.constant = CGFloat(arc4random_uniform(101)) - 50
      centerYConstraint.constant = CGFloat(arc4random_uniform(101)) - 50
      
      
      UIView.animate(withDuration: 0.3) { [weak self] in
         guard let strongSelf = self else { return }
         
         strongSelf.view.layoutIfNeeded()
      }
   }
   
   
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      // Do any additional setup after loading the view.
   }
}

```

```swift

class CHCRViewController: UIViewController {

   @IBOutlet weak var topLabel: UILabel!
   
   @IBOutlet weak var bottomLabel: UILabel!
   
   
   override func viewDidLoad() {
      super.viewDidLoad()
      
      let p = UILayoutPriority(rawValue: 250)
      topLabel.setContentHuggingPriority(p, for: .vertical)
   }
}

```
