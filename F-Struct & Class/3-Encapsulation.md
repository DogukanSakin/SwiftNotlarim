## Encapsulation

getter / setter syntaxı:

```swift
var myVar: String {
    get {
        return "Hello" // Burada değişkenin kendisini sonsuz döngü oluşmaması için kullanmamalıyız.
    }
    set (newValue) {
        print(newValue)
    }
}
```

Eğer yalnızca get yazılırsa değişkene hiçbir şekilde atama yapamayız. Benzer şekilde setlersek okuyamayız.