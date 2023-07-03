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

