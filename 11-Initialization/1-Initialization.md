## Initilazition

Initializers class, struct veya enumeration instance'larını oluşturmak için kullanılır. Swift'te initilazers bir değer döndürmez. Bir initilazer oluşturmak için:

```swift
init() {
    // initializer implementation goes here
}
```

Parametre eklemek gerekirse:

```swift
init(param1: Int, param2: String) {
    // initializer implementation goes here
}
```

Birden fazla initilazer oluşturmak için:

```swift
struct Color {
    let red, green, blue: Double
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
    init(white: Double) {
        red   = white
        green = white
        blue  = white
    }
}
```

Argüman label'larınının yazılmasını engellemek için diğer yerlerde kullanıldı gibi _ kullanılabilir:

```swift
struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
    init(_ celsius: Double) {
        temperatureInCelsius = celsius
    }
}
let bodyTemperature = Celsius(37.0)
// bodyTemperature.temperatureInCelsius is 37.0
```

Eğer optional bir değeri initilazer'da değer ataması yapmazsak otomatik olarak nil atanır.

Bir constant değere initilazer'da atama yapabiliriz:

```swift
class SurveyQuestion {
    let text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        print(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// Prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese."

//Daha sonrasında atama yapılamaz
cheeseQuestion.text = "Something else" // Error
```

Bir class'ın içerisinde değişkenlere default değer atanırsa initilazer oluşturmak zorunda değiliz:

```swift
class ShoppingListItem {
    var name: String?
    var quantity = 1
    var purchased = false
}
var item = ShoppingListItem()
```

Sturct'lar için initilazer'lar otomatik olarak oluşturulur:
```swift
struct Size {
    var width = 0.0, height = 0.0
}
let twoByTwo = Size(width: 2.0, height: 2.0)
```

Swift'te initializer'lar ikiye ayrılır: designated ve convenience.

## Designated Initializers

- Bir sınıfın temel başlatıcısıdır.
- Tüm özellikleri (stored properties) başlatır veya başlatmaz.
- Başka bir designated initializer'ı veya superclass'ın designated initializer'ını çağırabilir.
- init kelimesiyle başlar.
- İlgili nesnenin tam bir geçerli durumda olmasını sağlar.

```swift
class Person {
    let name: String
    let age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}
```

## Convenience Initializers

- Bir sınıfta (class) ekstra bir başlatıcı sağlar.
- Designated initializer'ları veya diğer convenience initializer'ları çağırır.
- Tüm özellikleri başlatmak zorunda değildir.
- convenience init şeklinde tanımlanır.

```swift
class Person {
    let name: String
    let age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    convenience init(name: String) {
        self.init(name: name, age: 0)
    }
}
```

## Initialization 2 Aşamalı Süreçtir

Swift'te initilazer'lar 2 aşamalıdır. İlk aşamada tüm stored property'lerin değerleri atanır. İkinci aşamada ise inherited class'ların initilazer'ları çağırılır. Bu aşamada tüm stored property'lerin değerleri atanmış olmalıdır.

```swift
class Vehicle {
    var numberOfWheels = 0
    var description: String {
        return "\(numberOfWheels) wheel(s)"
    }
}

let vehicle = Vehicle()
print("Vehicle: \(vehicle.description)")
// Vehicle: 0 wheel(s)
```

```swift
class Bicycle: Vehicle {
    override init() {
        super.init()
        numberOfWheels = 2
    }
}

let bicycle = Bicycle()
print("Bicycle: \(bicycle.description)")
// Bicycle: 2 wheel(s)
```

```swift
class Hoverboard: Vehicle {
    var color: String
    init(color: String) {
        self.color = color
        // super.init() implicitly called here
    }
    override var description: String {
        return "\(super.description) in a beautiful \(color)"
    }
}

let hoverboard = Hoverboard(color: "silver")
print("Hoverboard: \(hoverboard.description)")
// Hoverboard: 0 wheel(s) in a beautiful silver
```

Swift burada iki aşamalı initilazer'ın başlatılmasında hata olmadığından emin olmak için dört adet güvenlik önlemi alır:

- Bir nesne önce tüm depolama alanlarını (stored properties) geçerli bir değerle başlatmalıdır.
Bir nesnenin depolama alanları, uygun bir değerle başlatılmadan önce erişilemez durumdadır. Bu nedenle, initializer işlemi sırasında, bir nesne tüm depolama alanlarını geçerli bir değerle başlatmalıdır. Bu kurala uyulmadığında, derleme zamanında hata alırsınız.

- Bir sınıfın designated initializer'ı, üst sınıfının designated initializer'ını çağırmalıdır.
Bir sınıfın designated initializer'ı, üst sınıfının designated initializer'ını çağırmak zorundadır. Bu, sınıf hiyerarşisindeki tüm sınıfların geçerli bir durumda başlatılmış olmasını sağlar. Eğer üst sınıfın designated initializer'ı çağrılmazsa, derleme zamanında hata alırsınız.

- Bir convenience initializer, aynı sınıftaki başka bir initializer'ı çağırmalıdır.
Convenience initializer'lar, aynı sınıftaki başka bir initializer'ı çağırmak için kullanılmalıdır. Bu, initializer zincirlemesini sağlar ve tekrarlayan kodu önler. Convenience initializer, aynı sınıftaki başka bir initializer'ı çağırmazsa, derleme zamanında hata alırsınız.

- Bir initializer, tüm işlemler tamamlandıktan sonra self referansını kullanabilir.
Bir initializer, nesnenin depolama alanları ve diğer ayarlamaları tamamladıktan sonra self referansını kullanabilir. Bu nedenle, başka bir initializer çağrılmadan önce self referansını kullanmaya çalışırsanız, derleme zamanında hata alırsınız.


## İki Aşamadan Oluşan Initialization Süreci

İlk aşama sırasıyla:

- Bir class'ta belirlenmiş initializer çağırılır.

- Bir bellek alanı oluşturulur ancak henüz başlatılmaz.

- Designated initializer tüm özelliklerin bir değere sahip olduğunu onaylar ve bellek alanını başlatır.

- Designated initializer, üst sınıfın designated initializer'ını çağırır. Bu işlem inheritance zincirini takip ederek en üst sınıfa kadar devam eder.

- Zincirin en üstünde bulunan class'ında bir değere sahip olması sağlandığında 1. aşamanın tamamlandığı kabul edilir. 

İkinci aşama sırasıyla:

- Inheritence zincirinin tepesinden aşağıya doğru her class'ın convenience initializer'ları çağırılır. Artık class'lar self referansını kullanabilir.

- Son olarak en alttaki class'ın convenience initializer'ı çağırılır. 


## Otomatik Initializer'lar

Default olarak subclasslar superclass'ların initializer'larını inherit edemezler. Ancak bazı durumlarda subclass'ların içerisinde superclass'ların initializer'ları otomatik oluşur. Bu durumlar:

- Subclass'ta herhangi bir initializer tanımlanmamışsa.

- Subclass superclass'ta belirlenen tüm initializer'ları implement etmişse.

Örneğin:

```swift
class Vehicle {
    var numberOfWheels: Int
    
    init(numberOfWheels: Int) {
        self.numberOfWheels = numberOfWheels
    }
    
    convenience init() {
        self.init(numberOfWheels: 4)
    }
}

class Car: Vehicle {
    var brand: String
    
    init(brand: String, numberOfWheels: Int) {
        self.brand = brand
        super.init(numberOfWheels: numberOfWheels)
    }
}
```

Car sınıfı, üst sınıf olan Vehicle'ın designated initializer'ını override ederek kendi designated initializer'ını tanımlar. Ancak, convenience initializer'ı tanımlamaz.

Durum 2'ye göre, Car sınıfı, Vehicle sınıfının tüm designated initializer'larının bir implementasyonunu sağladığı için, Vehicle'ın convenience initializer'ını da otomatik olarak miras alır. Yani Car sınıfı aşağıdaki gibi bir şekilde oluşturulabilir:

```swift
let car = Car()
print(car.numberOfWheels) // Output: 4
```

## Required Initializer'lar

Bir superclass'ta subclass'ların implement etmesi gereken bir initializer varsa bunu required olarak belirlemek gerekir. Subclass'larda required olan bir initializer'ı override etmek için override anahtar kelimesini yazmaya gerek yoktur.

```swift
class SomeClass {
    required init() {
      
    }
}
class SomeSubclass: SomeClass {
    required init() {
        // direkt olarak bu şekilde override edilebilir.
    }
}
```