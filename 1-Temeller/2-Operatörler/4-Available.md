## Available

İşletim sistemi, platform ve derleme koşullarına göre kodun çalıştırılmasını sağlar.

```
@available(macOS 10.12, *)
struct ColorPreference {
    var bestColor = "blue"
}


func chooseBestColor() -> String {
    guard #available(macOS 10.12, *) else {
       return "gray"
    }
    let colors = ColorPreference()
    return colors.bestColor
}

```
```
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}

```

Ters kontrolde mümükün:

```
if #available(iOS 10, *) {
} else {
    // Fallback code
}


if #unavailable(iOS 10) {
    // Fallback code
}
```