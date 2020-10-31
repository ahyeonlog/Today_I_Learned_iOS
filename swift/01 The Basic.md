# [The Basic](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

## Constants and Variables

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

여러 상수, 또는 변수를 쉼표로 구분하여 한 줄에 선언 할 수 있다.

`var x = 0.0, y = 0.0, z = 0.0` 

>값이 변경되지 않으면 항상 `let` 키워드를 사용하여 상수로 선언한다. 변경할 수 있어야하는 값을 저장할 때만 변수를 사용한다.

## Type Annotations

```swift
var welcomeMessage: String
var red, green, blue: Double
```

변수나 상수를 정의할 때 초기 값을 제공하면 type annotations을 작성하지 않아도 Swift는 타입 추론을 할 수 있다.

## Naming Constants and Variables

변수 이름에 유니 코드 문자를 포함할 수 있다.

변수 이름에 공백 문자, 수학 기호, 화살표, 개인용 유니 코드 스칼라 값 또는 선 및 상자 그리기 문자는 포함될 수 없다. 숫자를 포함할 수 있지만 숫자로 시작할 수 없다.

## Printing Constants and Variables

```swift
print("friendlyWelcome is \(friendlyWelcome)")
```

## Integers

Swift는 부호있는 정수와 부호없는 정수를 8, 16, 32, 64 비트 형식으로 제공한다.

### Int

- 32비트 플랫폼에서 Int는 Int32와 같은 크기를 가진다.
- 64비트 플랫폼에서 Int는 Int64와 같은 크기를 가진다.

### UInt

플랫폼의 기본 단어 크기와 같은 부호없는 정수 유형이 필요한 경우에만 UInt를 사용한다. 

부호없는 8bit 정수 `UInt8`

```swift
let minValue = UInt8.min // equal to 0
let minValue = UInt8.max // equal to 255
```

## Floating-Point Numbers

Double은 소수점 이하 15자리의 정밀도를 갖고, Float은 소수점 이하 6자리의 정밀도를 가진다. 두 유형이 모두 적절한 상황에서도 Double이 선호된다.

## TypeAliases

```swift
typealias AudioSample = UInt
var maxAmplitudeFound = AudioSample.min
```

## Booleans

```swift
let orangesAreOrange = true
let turnipsAreDelicious = false
```

아래와 같은 경우는 컴파일 오류가 난다.

```swift
let i = 1
if i {
    // this example will not compile, and will report an error
}
```

## Tuples

튜플은 여러 값을 그룹화한다. 튜플 내의 값은 모든 유형이 될 수 있으며 각 항목이 동일한 유형일 필요는 없다.

```swift
let http404Error = (404, "Not Found")
//decompose
let (statusCode, statusMessage) = http404Error
//튜플의 일부만 필요할 땐 _로 무시할 수 있다.
let (justTheStatusCode, _) = http404Error
//index 번호로 접근할 수 있다.
print("The status code is \(http404Error.0)")
//각 요소의 이름을 지정할 수 있다.
let http200Status = (statusCode: 200, description: "OK")
print("The status code is \(http200Status.statusCode)")
print("The status message is \(http200Status.description)")
```

## Optionals

Swift의 `Int` 유형에는 String 값을 Int 값으로 변환하려고하는 이니셜 라이저가 있다. 문자열 "123"은 숫자 123으로 변환할 수 있지만 문자열 "hello world"에는 변환 할 명확한 숫자 값이 없다.

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
```

`convertedNumber` 은 이니셜라이저가 실패할 수 있으므로  Int가 아니라 `Int?` 를 반환한다.

### nil

값이 없는 상태로 설정한다. 옵셔널이 아닌 상수 및 변수에는 `nil` 을 사용할 수 없다. 기본값을 제공하지 않고 옵셔널 변수를 선언하면 자동으로 `nil` 로 설정된다.

Swift의 `nil` 은 존재하지 않는 객체에 대한 포인터가 아니라 특정 유형의 값이 없다는 것이다.

```swift
if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
```

옵셔널에 값이 포함된 것이 확실하면 `!` 를 뒤에 붙여서 값에 액세스 할 수 있다. 이것을 *forced unwrapping* 이라고 한다.

```swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
```

### Optional Binding

옵셔널 바인딩을 사용하여 옵셔널에 값이 있는지 확인하고 그 값을 임시 상수 또는 변수로 사용한다.

```swift
if let constantName = someOptional {
    statements
}
```

```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" could not be converted to an integer")
}
```

위의 코드는 다음과 같다. "Int(possibleNumber)에서 반환 된 옵셔널Int에 값이 있다면 actualNumber라는 새 상수에 그 값을 할당하시오" 

`Int(possibleNumber)` 가 성공한다면 actualNumber 상수는 if 문의 첫 번째 분기에서 사용할 수 있게 된다. 

하나의 if문에서 필요한 만큼의 옵셔널 바인딩과 Boolean 조건을 **쉼표** 로 구분할 수 있다.

```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Prints "4 < 42 < 100"
```

> if 문에서 옵셔널 바인딩으로 생성 된 상수 및 변수는 if 문의 본문 내에서만 사용할 수 있다. 반대로 guard문으로 생성된 상수와 변수는 guard문 다음에 오는 줄에서도 사용할 수 있다.

### Implicity Unwrapped Optionals(IUO)

옵셔널 값이 처음 설정된 경우에는 항상 값이 있음이 분명하다. 이러한 경우에는 값을 가지고 있다고 안전하게 가정할 수 있으므로 언래핑 과정을 제거할 수 있다.

```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation point

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation point
```

IUO는 non-optional 타입에 저장될 때 자동으로 언래핑된다. 위의 코드에서 `implicitString`은  String이고 non-optional이기 때문에 암시적으로 언래핑 된 옵셔널인 assumedString은 implicitString에 할당되기 전에 강제로 언래핑된다. 

```swift
let optionalString = assumedString
// The type of optionalString is "String?" and assumedString isn't force-unwrapped.
```

위와 같은 경우는 optionalString이 명시적인 타입이 없으므로 일반적인 옵셔널이 된다. 따라서 강제 언래핑되지 않는다.

암시적으로 언래핑된 옵셔널이 `nil` 인 값에 접근한다면 runtime error가 난다. 따라서 일반적인 옵셔널과 같은 방법으로 체크한다.

```swift
if assumedString != nil {
    print(assumedString!)
}
```

> 나중에 변수가 nil이 될 가능성이 있는 경우 IUO를 사용하지 않는다.

## Error Handling

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}
```

함수를 선언할 때 `throws` 키워드를 포함하여 오류가 발생할 수 있음을 나타낸다.

```swift
do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}
```

오류가 발생할 수 있는 함수를 호출할 때 표현식 앞에 `try` 키워드를 추가한다.  Swift는 `catch` 절에서 처리될 때 까지 오류를 전파한다. `do` 문은 하나 이상의 catch절에 오류를 전파할 수 있는 범위를 만든다.

```swift
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

`makeASandwich()` 함수는 깨끗한 접시를 사용할 수 없거나 재료가 없는 경우 오류를 발생시킨다. 오류가 발생할 수 있으므로 함수 호출은 `try` 표현식으로 래핑된다. 함수 호출을 `do`문으로 래핑하면 throw되는 모든 오류가 `catch`절에 전달된다.

오류가 발생하지 않으면 `eatASandwich()`함수가 호출된다. 오류가 발생하고 `SandwichError.outOfCleanDishes`와 일치하면 `washDishes()`함수가 호출된다. `SandwichError.missingIngredients`와 일치하면 cath 패턴에서 캡처한 연관된 [String] 값과 함께 `buyGroceries(_:)`함수가 호출된다.

