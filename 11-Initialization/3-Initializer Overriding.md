## Initializer Overriding

Swift'te subclass'lar default olarak superclass'ların initializer'ını kalıtım olarak almaz. Initializer'ı override etmek için belirli kurallar vardır:

- Alt sınıf, üst sınıfın designated initializer'ını override etmek için override anahtar kelimesini kullanmalıdır. Bu, alt sınıfın kendi implementasyonunu sağlar ve üst sınıftaki davranışı değiştirebilir. Override edilen başlatıcı, aynı parametreleri almalıdır ve super.init çağrısı ile üst sınıfın başlatıcısını çağırmalıdır.

- Convenience initializer'lar üst sınıftaki designated initializer'ı override edemez.
Convenience initializer'lar, sadece aynı sınıf içindeki başka bir başlatıcıyı veya üst sınıftaki convenience initializer'ı çağırabilir. Bu nedenle, bir alt sınıfın convenience initializer'ı, üst sınıftaki designated initializer'ı override edemez.

- Bir alt sınıf, üst sınıfın convenience initializer'ını override edebilir. Bu durumda, alt sınıfın convenience initializer'ı, üst sınıftaki convenience initializer'ı çağırırken override anahtar kelimesini kullanmalıdır.

- Bir başlatıcıyı override ederken, override edilen başlatıcının erişim düzeyi değiştirilebilir. Override eden başlatıcının erişim düzeyi, override edilen başlatıcının erişim düzeyinden daha yüksek olamaz.

Örnek:

```swift
class Person {
    let name: String

    init(name: String) {
        self.name = name
    }
}

class Employee: Person {
    let employeeID: String

    init(name: String, employeeID: String) {
        self.employeeID = employeeID
        super.init(name: name)
    }
}
```

subclass'lar override sonrası superclass'ın constant değerlerini değiştiremezler.

