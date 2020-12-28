decoder는 default로 Date로 디코딩한다.  
따라서 iso8601 format으로 바꾸고 싶다면 아래와 같이 직접 설정해주엉 한다.
```swift
let decoder = JSONDecoder()
decoder.dateDecodingStrategy = .iso8601
```

하지만 "2017-09-02T00:00:00"와 같이 마지막 Z가 빠져있는 경우에는?  
decoding하는 코드를 직접 구현하거나 decoding 전략을 커스텀해야 한다.  
후자의 방법을 살펴보겠다.  
```swift
let decoder = JSONDecoder()

decoder.dateDecodingStrategy = .custom({ (decoder) -> Date in
    let container = try decoder.singleValueContainer()
    let dateStr = try container.decode(String.self)
    
    let formatter = ISO8601DateFormatter()
    formatter.formatOptions = [.withFullDate, .withTime, .withDashSeparatorInDate, .withColonSeparatorInTime]
    
    return formatter.date(from: dateStr)!
})

```
