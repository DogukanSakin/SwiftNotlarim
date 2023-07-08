## Memory Safety

Swift çoğu durumda bellek yönetimini otomatik olarak kontrol eder. Ancak bazı durumlarda bellek erişiminde conflict çıkması durumunda run-time hataları almak mümkündür. 

## Bellek Erişimindeki Conflict

Swift'te belleğe erişim bir değişkenin değerini değiştirmek, okumak veya bir fonksiyona parametre geçirmek gibi durumlarda gerçekleşir. Conflict, kodun farklı bölümlerinin aynı anda aynı bellek konumuna erişmeye çalıştığında gerçekleşebilir. Özellikle multithread kod yazarken bu sorunla karşılaşmak olasıdır.

## Bellek Erişim Conflict'inin Karakteristiği

Bellek erişiminde conflict için dikkate alınması gereken üç durum vardır:

- Erişim işlemi read veya  write işlemi mi?
- Erişim işlemi hangi bellek konumuna yapılıyor?
- Erişimin süresi ne kadar?

Özellikle aşağıdaki koşullar altında iki kez erişime sahipsek conflict oluşur:

- Erişimlerden biri write işlemi ise
- Erişimler aynı bellek konumuna yapılıyorsa
- Erişim süreleri aynıysa

## inout Parametrelerinde Conflict

Bir fonksiyon inout paramterleri için long term write işlemine sahiptir. Birden çok inout parametreye sahip bir fonksiyon varsa write erişimleri parametrelerin görüntülendiği sırada başlar. inout parametresi olarak geçirilen değerlere aynı anda birden fazla erişim yapma girişimi conflict'e neden olur. Fonksiyon parametresi inout olarak işaretlendiğinde, bu parametrenin değeri fonksiyonun çalışma süresince değiştirilebilir. inout parametresi, bir değeri işaret eden bir referans gibi davranır. Birden fazla eşzamanlı erişim, doğru bir şekilde yönetilmediğinde hatalara ve beklenmeyen sonuçlara neden olabilir.

Örneğin:

```swift
func increment(_ number: inout Int) {
    number += 1
}

var value = 5
increment(&value)

var value = 5
increment(&value)
increment(&value)
// Error: Conflicting accesses to value
```

Bu örnekte, increment fonksiyonuna &value ifadesiyle bir referans geçildi. İkinci increment çağrısında ise aynı referansın tekrar kullanılmasıyla çakışan erişim oluşur ve derleme zamanında hata üretilir.
 

## Fonksiyon İçerisinde Self Kullanımında Conflict

self referansına aynı anda birden fazla erişim yapma girişimi yapılırsa conflict oluşur.  Örneğin, aşağıdaki kod parçasında, bir sınıf içindeki bir metodun self referansına erişim yapılmaktadır:

```swift
class Counter {
    private var count = 0
    
    func increment() {
        count += 1
    }
    
    func incrementTwice() {
        increment()
        increment()
    }
}
```

Ancak, aşağıdaki gibi bir çakışan erişim durumunda hatalar oluşabilir:

```swift
let counter = Counter()
counter.incrementTwice()
// Error: Conflicting accesses to self in methods
```

## Property'lerde Conflict

Benzer şekilde property'lere aynı anda birden fazla erişim yapma girişimi yapılırsa conflict oluşur. Swift dilinde, bir sınıfın veya yapının özelliklerine erişim, bir getter veya setter metodu aracılığıyla gerçekleştirilir. Özelliklere yapılan erişimlerin senkronize bir şekilde gerçekleşmesi önemlidir. Birden fazla eşzamanlı erişim, doğru bir şekilde yönetilmediğinde hatalara ve beklenmeyen sonuçlara neden olabilir.

Örneğin, aşağıdaki kod parçasında, bir sınıfın özelliğine aynı anda birden fazla erişim yapma girişimini görebiliriz:

```swift
class Counter {
    private var count = 0
    
    var value: Int {
        get {
            return count
        }
        set {
            count = newValue
        }
    }
    
    func increment() {
        value += 1
    }
    
    func incrementTwice() {
        value += 1
        value += 1
    }
}
```

Ancak, aşağıdaki gibi bir çakışan erişim durumunda hatalar oluşabilir:
    
```swift
let counter = Counter()
counter.incrementTwice()
// Error: Conflicting accesses to value
```
Bu örnekte, incrementTwice metodunun içinde value özelliğine iki kez erişim yapılır. Ancak, aynı anda birden fazla erişim yapıldığı için çakışan erişim hatası oluşur ve derleme zamanında hata üretilir.