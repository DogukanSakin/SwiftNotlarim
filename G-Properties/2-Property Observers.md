## Property Observers

Property Observers" (Özellik Gözlemcileri), bir saklanan özelliğin değeri değiştiğinde otomatik olarak gerçekleştirilecek eylemleri tanımlamamıza olanak sağlar. Property Observers, bir özelliğin değerindeki değişiklikleri izlememize ve bu değişiklikler üzerinde özel kod blokları çalıştırmamıza olanak tanır.

Swift'te iki tür Property Observer bulunur: "willSet" ve "didSet".

## willSet

"willSet" Property Observer, bir saklanan özelliğin değeri ayarlanmadan önce çalışır. Bu observer, yeni değeri ve değişkenin varsayılan ismi olan "newValue" aracılığıyla erişebilir. "willSet" bloğu, yeni değerin atanmadan önce kontrol edilmesi, işlenmesi veya geçerliliğinin doğrulanması gibi eylemleri gerçekleştirmek için kullanılabilir. Hiçbir parametre eklenmezse default olarak "newValue" kullanılır.

```swift
class User {
    var name: String {
        willSet {
            print("New name: \(newValue)")
        }
    }
    
    init(name: String) {
        self.name = name
    }
}

let user = User(name: "John")
user.name = "Jane"
// Çıktı: New name: Jane
```

## didSet

"didSet" Property Observer, bir saklanan özelliğin değeri ayarlandıktan sonra çalışır. Bu observer, önceki değere "oldValue" aracılığıyla erişebilir. "didSet" bloğu, önceki değere dayalı olarak değişiklik sonrası işlemleri gerçekleştirmek için kullanılabilir. Hiçbir parametre eklenmezse default olarak "oldValue" kullanılır.

```swift
class Counter {
    var count: Int = 0 {
        didSet {
            print("Count changed from \(oldValue) to \(count)")
        }
    }
    
    func increment() {
        count += 1
    }
}

let counter = Counter()
counter.increment()
// Çıktı: Count changed from 0 to 1
```

