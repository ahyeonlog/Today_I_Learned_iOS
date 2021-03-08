```swift
  @IBAction func switchMode(_ sender: Any) {
      let currentMode = imageView.contentMode.rawValue

      let newMode = UIView.ContentMode(rawValue: currentMode + 1) ?? .scaleAspectFit
      imageView.contentMode = newMode
      updateModeLabel()
  }

  func updateModeLabel() {
      switch imageView.contentMode {
      case .scaleToFill:
          modeLabel.text = "Scale to fill"
      case .scaleAspectFit:
          modeLabel.text = "Aspect fit"
      case .scaleAspectFill:
          modeLabel.text = "Aspect fill"
      case .redraw:
          modeLabel.text = "Redraw"
      case .center:
          modeLabel.text = "Center"
      case .top:
          modeLabel.text = "Top"
      case .bottom:
          modeLabel.text = "Bottom"
      case .left:
          modeLabel.text = "Left"
      case .right:
          modeLabel.text = "Right"
      case .topLeft:
          modeLabel.text = "Top left"
      case .topRight:
          modeLabel.text = "Top right"
      case .bottomLeft:
          modeLabel.text = "Bottom left"
      case .bottomRight:
          modeLabel.text = "Bottom right"
      @unknown default:
          fatalError()
      }
  }
```
