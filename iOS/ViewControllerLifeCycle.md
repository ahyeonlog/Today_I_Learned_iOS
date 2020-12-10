override func viewDidLoad() {
super.viewDidLoad()
print(className, #function)
}
override func viewWillAppear(_ animated: Bool) {
super.viewWillAppear(animated)
print(className, #function)
}
override func viewDidAppear(_ animated: Bool) {
super.viewDidAppear(animated)
print(className, #function)
}
override func viewWillDisappear(_ animated: Bool) {
super.viewWillDisappear(animated)
print(className, #function)
}
override func viewDidDisappear(_ animated: Bool) {
super.viewDidDisappear(animated)
print(className, #function)
}
deinit {
print(className, #function)
}



