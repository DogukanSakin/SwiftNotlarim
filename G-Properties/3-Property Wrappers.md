## Property Wrappers

Swift 5.1 ile birlikte tanıtılan "Property Wrappers" (Özellik Sarmalayıcılar), property'lerin davranışını özelleştirmek ve tekrar kullanılabilirliği artırmak için kullanılan bir özelliktir. Property Wrappers, bir property'i sarmalayarak, property'nin değer ataması, erişimi ve depolanması gibi işlemleri kontrol etmemizi sağlar.

Property Wrappers, property'lerin üzerine uygulanır ve property'lerin işlevselliğini değiştirmek veya genişletmek için kullanılır. Bu sayede, tekrar eden kod bloklarını azaltabilir ve property'leri daha okunabilir ve sade hale getirebiliriz.

Bir Property Wrapper oluşturmak için, @propertyWrapper adlandırılmış bir struct veya class tanımlamamız gerekmektedir. Property Wrapper, wrappedValue adında bir özellik sağlar ve wrappedValue üzerinde işlemler gerçekleştirerek özelliğin davranışını değiştirebilir.

```swift
@propertyWrapper
struct Trimmed {
    private(set) var value: String = ""

    var wrappedValue: String {
        get { value }
        set { value = newValue.trimmingCharacters(in: .whitespacesAndNewlines) }
    }

    init(wrappedValue: String) {
        self.wrappedValue = wrappedValue.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}

struct User {
    @Trimmed var name: String
}

let user = User(name: "  John  ")
print(user.name) // "John"
```
Yukarıdaki örnekte, "Trimmed" adında bir Property Wrapper oluşturulmuştur. Bu Property Wrapper, bir String değerini alırken başında ve sonunda bulunan boşlukları temizleyen bir işlevselliği sağlar. "Trimmed" yapısı bir wrappedValue özelliği sağlar ve bu özelliği üzerinde işlem yaparak değerleri işler.

"User" yapısında, "name" özelliği @Trimmed Property Wrapper ile sarmalanmıştır. Böylece, "name" özelliğine atanan değer otomatik olarak boşlukları temizlenir. Örnekte, "user.name" ifadesiyle "name" özelliği atanırken başında ve sonunda bulunan boşluklar temizlenir ve "John" olarak döndürülür.

Property Wrappers, property'leri özelleştirmek, doğrulama yapmak, geçerlilik kontrolü yapmak veya özellik değerlerini otomatik olarak dönüştürmek gibi durumlarda oldukça kullanışlıdır. Ayrıca, kod tekrarını azaltır ve daha okunabilir, sade bir kod yazmamızı sağlar.

## Property Wrappers ve Init

Bazı durumlarda Wrapper'da property'e bir değer verilmediğinde init ile bir değer vermek isteyebiliriz. Bunun için init fonksiyonunu kullanabiliriz.

```swift
@propertyWrapper
struct MyWrapper {
    private var value: Int

    var wrappedValue: Int {
        get { value }
        set { value = newValue }
    }

    init(wrappedValue initialValue: Int) {
        self.value = initialValue
    }
}

struct MyStruct {
    @MyWrapper(wrappedValue: 20) var myProperty: Int
}

let myStruct = MyStruct()
print(myStruct.myProperty) // 20
```

## Property Wrappers'ta Projecting

Property Wrapper'ın sarmaladığı özelliğin üzerinden ek bilgiler veya işlemler sağlamak için kullanılır. Projecting, Property Wrapper yapısının üzerinde tanımlanan bir özelliğe erişmeyi ve o özellik üzerinde belirli işlemler gerçekleştirmeyi mümkün kılar. 

```swift
@propertyWrapper
struct MyWrapper<Value> {
    private var value: Value

    var wrappedValue: Value {
        get { value }
        set { value = newValue }
    }

    var projectedValue: String {
        return "Projected value: \(value)"
    }

    init(initialValue: Value) {
        self.value = initialValue
    }
}

struct MyStruct {
    @MyWrapper(initialValue: 10) var myProperty: Int
}

let myStruct = MyStruct()
print(myStruct.$myProperty) // Projected value: 10
```

Yukarıdaki örnekte, "MyWrapper" adında bir Property Wrapper tanımlanmıştır. Bu Property Wrapper, bir değeri saklar ve wrappedValue özelliği üzerinde işlemler gerçekleştirir. Ayrıca, "projectedValue" adında bir özellik tanımlanmıştır. Bu özellik, sarılmış özelliğin üzerinden projection yapılacak değeri temsil eder.

"MyStruct" adında bir yapı tanımlanmıştır ve "myProperty" adında bir sarılmış özellik içerir. Bu sarılmış özelliğin üzerinden projection yapmak için "$" sembolü kullanılır ve projection yapılan değer elde edilir.

Sonuç olarak, "myStruct.$myProperty" ifadesi kullanıldığında, sarılmış özelliğin projection değeri olan "Projected value: 10" elde edilir ve yazdırılır.

