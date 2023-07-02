## Override

Override veya overwriting bir sınıf tarafından kalıtım almış başka bir sınıfın kalıtımla aldığı özelliklerin veya methodların kendi içerisinde değiştirilmesidir. Override işlemi için override keyword'ü kullanılır.

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

class Car : Vehicle {
    var gear = 1
    override var description: String {
        return super.description + " in gear \(gear)"
    }
}
```

## getter/setter Override

```swift
class Superclass {
    var myProperty: Int {
        get {
            return 10
        }
        set {
            print("Superclass set")
        }
    }
}

class Subclass: Superclass {
    override var myProperty: Int {
        get {
            return super.myProperty + 5
        }
        set {
            print("Subclass set")
        }
    }
}

let obj = Subclass()
print(obj.myProperty) // Output: 15
obj.myProperty = 20 // Output: "Subclass set"
```

Override edilmiş bir özelliğin yalnızca get veya set gözlemcilerini kullanmak:

```swift
class Superclass {
    var myProperty: Int {
        get {
            return 10
        }
        set {
            print("Superclass set")
        }
    }
}

class Subclass: Superclass {
    override var myProperty: Int {
        get {
            return super.myProperty + 5
        }
    }
}

let obj = Subclass()
print(obj.myProperty) // Output: 15
obj.myProperty = 20 // Error: Cannot assign to property: 'myProperty' is a get-only property
```

Bu örnekte, Subclass alt sınıfı, myProperty adlı özelliğin sadece get gözlemcisini override etmiştir. Set gözlemcisi override edilmemiştir ve alt sınıfta özelliğin sadece okunabilir (get-only) olduğu bir durum oluşmuştur.

## super

super keyword'ü ile override edilmiş bir özelliğin veya methodun superclass'ındaki orijinal haline erişilebilir.

```swift
class Superclass {
    func myMethod() {
        print("Superclass")
    }
}

class Subclass: Superclass {
    override func myMethod() {
        super.myMethod()
        print("Subclass")
    }
}

let obj = Subclass()

obj.myMethod() // Output: Superclass
               //         Subclass
```

## Property Observes Override

```swift
class Superclass {
    var myProperty: Int = 0 {
        willSet {
            print("Superclass willSet - New value: \(newValue)")
        }
        didSet {
            print("Superclass didSet - Old value: \(oldValue), New value: \(myProperty)")
        }
    }
}

class Subclass: Superclass {
    override var myProperty: Int {
        willSet {
            print("Subclass willSet - New value: \(newValue)")
        }
        didSet {
            print("Subclass didSet - Old value: \(oldValue), New value: \(myProperty)")
        }
    }
}

let obj = Subclass()
obj.myProperty = 5
// Output:
// Superclass willSet - New value: 5
// Superclass didSet - Old value: 0, New value: 5
// Subclass willSet - New value: 5
// Subclass didSet - Old value: 0, New value: 5

obj.myProperty = 10
// Output:
// Superclass willSet - New value: 10
// Superclass didSet - Old value: 5, New value: 10
// Subclass willSet - New value: 10
// Subclass didSet - Old value: 5, New value: 10
```

Not: setter'a sahip olmayan bir özelliğin willSet ve didSet gözlemcileri override edilemez.

## init() Override

```swift
class Superclass {
    let constantProperty: Int = 10 // Inherited constant stored property
    
    var readOnlyProperty: Int { // Inherited read-only computed property
        return 20
    }
}

class Subclass: Superclass {
    override var constantProperty: Int {
        didSet {
            print("Subclass didSet - New value: \(constantProperty)")
        }
    }
    
    override var readOnlyProperty: Int {
        didSet {
            print("Subclass didSet - New value: \(readOnlyProperty)")
        }
    }
    // Error: Cannot override with a stored property 'constantProperty' with a setter
    // Error: Property does not override any property from its superclass
}
```

## final

final keyword'ü ile bir sınıfın veya sınıfın özelliğinin veya methodunun override edilmesi engellenebilir.

```swift
class Superclass {
    final func myMethod() {
        print("Superclass")
    }
}

class Subclass: Superclass {
    override func myMethod() { // Error: Cannot override 'final' method
        print("Subclass")
    }
}
```

```swift

