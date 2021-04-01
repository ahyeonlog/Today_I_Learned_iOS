```swift
override func willTransition(to newCollection: UITraitCollection, with coordinator: UIViewControllerTransitionCoordinator) {
    super.willTransition(to: newCollection, with: coordinator)

    switch (newCollection.horizontalSizeClass, newCollection.verticalSizeClass) {
    case (.regular, .regular):
        contentTextView.font = UIFont.systemFont(ofSize: 30)
    default:
        contentTextView.font = UIFont.systemFont(ofSize: 20)
    }
    print("======================")
}
```
