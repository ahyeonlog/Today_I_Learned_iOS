```swift
let stringDate: String = "2020-11-09T11:05:56.000Z"

let iso8601DateFormatter = ISO8601DateFormatter()
iso8601DateFormatter.formatOptions = [.withInternetDateTime, .withFractionalSeconds]
let date = iso8601DateFormatter.date(from: stringDate)


let formatter = DateFormatter()
formatter.dateFormat = "yyyy. MM. dd"

label.text = formatter.string(for: date!)
```
