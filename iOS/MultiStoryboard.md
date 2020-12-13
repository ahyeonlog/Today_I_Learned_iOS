

```swift
@IBAction func presentModalVC(_ sender: Any) {
    // StoryBoard 파일 이름, Storyboard가 포함된 번들 이름
    let subStoryboard = UIStoryboard(name: "Sub", bundle: nil)
    guard let vc = subStoryboard?.instantiateViewController(identifier: "modalVC") else { return }
    present(vc, animated: true, completion: nil)
}

```
