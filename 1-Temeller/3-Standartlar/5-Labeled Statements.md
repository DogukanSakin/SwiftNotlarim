## Labeled Statements

Bir döngü veya switch ifadesine isim vermek için kullanılır. Break ve continue ifadelerinde doğrudan bu isim eklenerek yalnızca istediğimiz döngü veya switch ifadesinden çıkabiliriz.

```swift
outerLoop: for i in 1...10 {
    for j in 1...10 {
        let product = i * j
        if product == 50 {
            print("50 bulundu!")
            break outerLoop
        }
    }
}
```

