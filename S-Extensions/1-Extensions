## Extensions

Extension'lar class'lara, struct'lara, enum'lara veya protocol'lere yeni işlevsellik kazandırmak için kullanılan bir yapıdır. Extension'ların kaynak kodların erişilmediği durumda da yapının genişletilmesine izin verir.

Extension'lar şunları yapabilir:

- Yeni hesaplanmış property'ler ve hesaplanmış property'lerin getter ve setter'ları tanımlayabilir.
- Yeni instance method'lar ve type method'lar tanımlayabilir.
- Yeni initializer'lar tanımlayabilir.
- Subscript'ler tanımlayabilir.
- Yeni nested type'lar tanımlayabilir.
- Var olan bir türün protokol uygulamasını genişletebilir.

Extension'lar yeni fonksiyonellikler eklerken var olan fonksiyonları override edemez.

Temel syntax:

```swift
extension SomeType {
    // new functionality to add to SomeType goes here
}
```

Extension'lar birden fazla protocol'ü uygulayabilir. Bu durumda, protocol'ler arasında virgülle ayrılmış bir liste kullanılır:

```swift
extension SomeType: SomeProtocol, AnotherProtocol {
    // protocol implementations go here
}
```

## Extensions - Initializers

Extension'lar ile yeni initializer'lar tanımlanabilir. Bu initializer'lar, extension'ın tanımlandığı türün tüm instance'ları için kullanılabilir. Extension içerisinde tanımlanan initializer'lar orijinal türün initializer'ı üzerinde bir değişiklik yapamaz. Bunun yerine, extension'ın initializer'ı, orijinal türün initializer'ını çağırır.

Temel syntax:

```swift
extension SomeType {
    init(parameters) {
        // initializer implementation goes here
    }
}
```

## Extensions - Methods

Extension'lar ile yeni instance method'lar ve type method'lar tanımlanabilir. Örneğin:

```swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}

3.repetitions {
    print("Hello!")
}
// Hello!
// Hello!
// Hello!
```
