## Inheritance 

Inheritance yani kalıtım bir class'ın başka bir class'tan özelliklerini almasıdır. Kalıtım alınan class'a **superclass** denir. Kalıtım veren class'a ise **subclass** denir. Hiçbir inheritance işlemi yapılmamış class'lar **base class** olarak adlandırılır. Swift çoklu kalıtımı desteklemez.

Kalıtım için basitçe : operatorü kullanılır.

```swift
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // do nothing - an arbitrary vehicle doesn't necessarily make a noise
    }
}

class Car: Vehicle { // Car class'ı Vehicle class'ından kalıtım aldı.
    
}
```