```swift
class TimerViewController: UIViewController {
    
    @IBOutlet weak var timeLabel: UILabel!
    
    lazy var formatter: DateFormatter = {
        let f = DateFormatter()
        f.dateFormat = "hh:mm:ss"
        return f
    }()
    
    @IBAction func unwindToTimerHome(_ sender: UIStoryboardSegue) {
        
    }
    
    func updateTimer(_ timer: Timer) {
        print(#function, Date(), timer)
        timeLabel.text = formatter.string(from: Date())
    }
    
    func resetTimer() {
        timeLabel.text = "00:00:00"
    }
    
    var timer: Timer?
    
    @objc func timerFired(_ timer: Timer) {
        updateTimer(timer)
    }
    
    @IBAction func startTimer(_ sender: Any) {
        // 이미 실행 중인 타이머가 있다면 새롭게 생성되는 것을 막기
        guard timer == nil else { return }
        
        // 1. 타입 매소드로 타이머 생성
        // param: 반복주기, 반복, 반복적으로 실행할 코드
        timer = Timer.scheduledTimer(withTimeInterval: 1, repeats: true, block: { (timer) in
            guard timer.isValid else { return }
            self.updateTimer(timer)
        })
        
        // 2. 생성자로 타이머 생성
        // 런루프에 타이머를 추가한 후 fire 매소드를 실행해야 함
        timer = Timer(timeInterval: 1, target: self, selector: #selector(timerFired(_:)), userInfo: nil, repeats: true)
        // tolerance : 타이머는 오차 없이 동작하는 것이 아니다. 하지만 허용오차를 적용하면 ios가 실행주기를 조절한다. 이런 최적화를 통해서 배터리를 절약하고 응답성을 향상시킨다.
        timer?.tolerance = 0.2
        RunLoop.current.add(timer!, forMode: .defaultRunLoopMode)
        timer?.fire()
    }
    
    @IBAction func stopTimer(_ sender: Any) {
        // timer를 런루프에서 제거
        // 제거된 타이머는 다시 사용할 수 없고, 작업을 해야 한다면 다시 타이머를 생성해야 함
        // 주의할 점은 타이머가 생성된 곳과 동일한 스레드에서 호출해야 한다. 그렇지 않으면 타이머가 정상적으로 중지되지 않는다.
        timer?.invalidate()
        
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        resetTimer()
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        
        startTimer(self)
    }
    
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        // 화면을 벗어날 때 타이머 없애기
        timer?.invalidate()
        timer = nil
    }
}

```

타이머를 사용할 때에는 적절한 곳에 `invalidate` 메소드를 호출해서 리소스가 낭비되는 것을 막아야 함을 주의하자!
