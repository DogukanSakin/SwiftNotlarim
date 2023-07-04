## Deinit

Bir class'ın deinit fonksiyonu, class'ın bir instance'ı yok edilirken çağrılır. Deinitler yalnızca class'larda kullanılabilir. Swift, bir instance'a artık ihtiyaç olmazsa bu işlemi otomatik olarak yapar. Ancak bazı durumlarda bizim bellek yönetimi için manuel olarak bu işlemi yapmamız gerekebilir. Deinit herhangi bir parametre almaz ve parantezsiz yazılır.

```swift
class SomeClass {
    deinit {
        // perform the deinitialization
    }
}
```

Inheritance olarak deinit superclass'tan subclass'lara doğru aktarılır. Superclass'ların deinit'leri subclass'larda tanımlanmasa bile her zaman çağırılır.

