# 🧩 [View Controller의 역할](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/index.html#//apple_ref/doc/uid/TP40007457)

뷰 컨트롤러는 앱 내부 구조의 기초이다.  모든 앱에는 하나 이상의 뷰 컨트롤러를 가지고 있다. 뷰 콘트롤러의 역할은 다음과 같다.

1. View Management
2. Data Marshaling
3. User Interactions
4. Resource Management
5. Adaptivity

### View Manangement

뷰 컨트롤러의 가장 중요한 역할을 뷰 계층을 관리하는 것이다. 모든 뷰 컨트롤러에는 모든 컨텐츠를 포함하는 단일 루트 뷰가 있다. 해당 루트 뷰에 컨텐츠를 표시할 뷰를 추가한다.

![뷰 컨트롤러와 뷰의 관계](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/Art/VCPG_ControllerHierarchy_fig_1-1_2x.png)



뷰 컨트롤러는 두 가지 타입이 존재한다.

- Content View Controller 
- Container View Controller

컨텐츠 뷰 컨트롤러는 모든 뷰를 자체적으로 관리한다. 컨테이너 뷰 컨트롤러는 자체 뷰와 하나 이상의 자식 뷰 컨트롤러의 루트 뷰를 관리한다. 여기에서 컨테이너는 자식의 컨텐츠를 관리하지 않는다는 점을 주의해야한다. 자식의 루트 뷰만 관리하고 컨테이너의 디자인에 따라 크기를 조정하고 배치한다.

### Data Marshaling

뷰 컨트롤러는 관리하는 뷰와 앱 데이터 사이에서 중개자 역할을 한다. 

### User Interactions

뷰 컨트롤러는 `UIResponder` 객체이며 일반적으로 다른 뷰 컨트롤러에 속하는 루트 뷰와 해당 뷰의 슈퍼 뷰 사이의 응답자 체인에 삽입된다. 뷰 컨트롤러는 응답자 체인에서 내려 오는 이벤트를 처리할 수 있지만 뷰 컨트롤러는 터치 이벤트를 직접 처리하는 경우는 거의 없다. 일반적으로 뷰가 자체 터치 이벤트를 처리하고, 델리게이트 또는 대상 객체의 메소드에 결과를 보고한다.  뷰 컨트롤러의 뷰가 이벤트를 처리하지 않으면 뷰 컨트롤러가 이벤트를 처리하거나 슈퍼 뷰에 전달할 수 있다.

### Resource Management

뷰 컨트롤러는 대부분의 뷰 관리를 자동으로 처리한다. 예를 들어 사용 가능한 메모리가 부족하면 UIKit은 앱에 더 이상 필요하지 않은 리소스를 확보하도록 요청한다. 한 가지 방법은 뷰 컨트롤러의 `didReceiveMemoryWarning` 메서드를 호출하는 것이다. 이 방법으로 더 이상 필요하지 않거나 나중에 쉽게 다시 만들 수 있는 개체에 대한 참조를 제거한다. 메모리 부족 상태가 발생하면 가능한 많은 메모리를 해제하는 것이 중요하다. 메모리를 너무 많이 사용하는 앱은 시스템에서 메모리를 복구하기 위해 완전히 종료될 수 있다.

### Adaptivity

뷰 컨트롤러는 뷰를 환경에 맞게 조정하는 일을 담당한다. 모든 iOS 앱은 iPad 및 다양한 크기의 iPhone에서 실행할 수 있어야 한다. 기기별로 서로 다른 뷰 컨트롤러 및 뷰 계층을 제공하는 대신 변화하는 환경에 맞게 뷰를 조정하는 단일 뷰 컨트롤러를 사용하는 것이 더 간편하다.



