```swift
override func viewDidLoad() {
    super.viewDidLoad()

    redView.translatesAutoresizingMaskIntoConstraints = false

    if #available(iOS 11.0, *) {
        redView.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor).isActive = true
        redView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor).isActive = true
        redView.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor).isActive = true
        redView.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor).isActive = true

        print(view.safeAreaInsets)
        additionalSafeAreaInsets = UIEdgeInsets(top: 10, left: 10, bottom: 10, right: 10)
    } else {
        redView.leadingAnchor.constraint(equalTo: view.leadingAnchor).isActive = true
        redView.topAnchor.constraint(equalTo: topLayoutGuide.bottomAnchor).isActive = true
        redView.bottomAnchor.constraint(equalTo: bottomLayoutGuide.topAnchor).isActive = true
        redView.trailingAnchor.constraint(equalTo: view.trailingAnchor).isActive = true
    }
}
```
