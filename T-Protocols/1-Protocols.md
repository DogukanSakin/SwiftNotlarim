## Protocols

Protocol'ler, bir türün belirli bir işlevselliği veya özelliği uygulamasını sağlar. Bir protocol, bir veya birden fazla property, method, initializer veya subscript tanımlayabilir. Bir tür, bir protocol'ü uyguladığında, tür, protocol'ün tüm gereksinimlerini karşılamalıdır.

Temel syntax:

```swift
protocol SomeProtocol {
    // protocol definition goes here
}
```

Bir class, protocol vs. birden fazla protocol'ü uygulayabilir. Bu durumda, protocol'ler arasında virgülle ayrılmış bir liste kullanılır:

```swift
struct SomeStructure: FirstProtocol, AnotherProtocol {
    // structure definition goes here
}

class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
    // class definition goes here
}
```

Protocol'e bir property eklemek istersek:

```swift
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
    static func someTypeMethod()
}
```

Burada protocol içerisinde tanımlanan property her türe özgü olmayacaksa `static` keyword'ü kullanılabilir. Bu durumda, property'ye erişmek için türün adı kullanılır:

```swift
protocol AnotherProtocol {
    static var someTypeProperty: Int { get set }
}
```

## Protocol'ler ve Initializer'lar

Bir protocol, initializer tanımlayabilir. Bir tür, protocol'ü uyguladığında, tür, protocol'ün initializer'ını uygulamalıdır. Bir initializer, initializer'ı uygulayan türün initializer'ını override edemez.

```swift
protocol SomeProtocol {
    init(someParameter: Int)
}
```

Eğer aynı anda hem bir superclass'ın hem de bir protocol'ün initializer'ı uygulanmak isteniyorsa required ve override keyword'leri kullanılır:

```swift
protocol SomeProtocol {
    init()
}

class SomeSuperClass {
    init() {
        // initializer implementation goes here
    }
}

class SomeSubClass: SomeSuperClass, SomeProtocol {
    // "required" from SomeProtocol conformance; "override" from SomeSuperClass
    required override init() {
        // initializer implementation goes here
    }
}
```

Protocol'ler extension'lar ile de kullanılabilir:

```swift
protocol TextRepresentable {
    var textualDescription: String { get }
}

extension Dice: TextRepresentable {
    var textualDescription: String {
        return "A \(sides)-sided dice"
    }
}
```

Bir protocol extension ile genişletilebilir:

```swift
protocol MyProtocol {
    func someMethod()
}

extension MyProtocol {
    func someMethod() {
        print("Default implementation of someMethod")
    }
    
    func additionalMethod() {
        print("Additional method provided by the extension")
    }
}

struct MyStruct: MyProtocol {
    // MyProtocol'ün gerekliliklerini otomatik olarak karşılar
}

let myStruct = MyStruct()
myStruct.someMethod()          // Default implementation of someMethod
myStruct.additionalMethod()    // Additional method provided by the extension

```

Bir protocol bir veya daha fazla protocol'ü inherit edebilir:

```swift
protocol InheritingProtocol: SomeProtocol, AnotherProtocol {
    // protocol definition goes here
}
```

## Class-Only Protocols

Bir protocol, sadece class'lar tarafından uygulanabilirse, class-only protocol olarak adlandırılır. Bir protocol'ü class-only yapmak için, protocol'ün inheritance listesinin başına `AnyObject` keyword'ü eklenir:

```swift
protocol SomeClassOnlyProtocol: class, SomeInheritedProtocol {
    // class-only protocol definition goes here
}
```

## Protocol İçerisinde Optional Gereksinimler

Bir protocol, optional gereksinimler tanımlayabilir. Bu gereksinimler, uygulayan tür tarafından uygulanmayabilir. Bir optional gereksinim, `optional` keyword'ü ile tanımlanır. Bir optional gereksinim, `?` ile işaretlenmiş bir property veya method olabilir. Bir optional gereksinim, `optional` keyword'ü ile tanımlanmış bir initializer olamaz.

```swift
@objc protocol CounterDataSource {
    @objc optional func increment(forCount count: Int) -> Int
    @objc optional var fixedIncrement: Int { get }
}
```

## Protocol Extension'larında Kısıtlayıcılar

Swift'te bir protocol'ü genişletmek için extension yazarken kısıtlamalar yani constraint'ler oluşturmaya izin verir.Protokol genişletmeleri, protokolü uygulayan tüm tipler için ortak uygulamalar sağlar. Ancak, bazen genişlemeyle sağlanan işlevselliğin belirli tiplerle sınırlanması gerekebilir. Bu durumda bu yönteme başvurulabilir.

```swift
protocol MyProtocol {
    func someMethod()
}

extension MyProtocol where Self: SomeClass {
    func someMethod() {
        print("SomeClass implementation of someMethod")
    }
}

class SomeClass: MyProtocol {
    // MyProtocol'ün gerekliliklerini otomatik olarak karşılar
}

struct SomeStruct: MyProtocol {
    // MyProtocol'ün gerekliliklerini otomatik olarak karşılamaz
}

let someClass = SomeClass()
someClass.someMethod()       // SomeClass implementation of someMethod

let someStruct = SomeStruct()
someStruct.someMethod()      // Default implementation of someMethod
```

Yukarıdaki örnekte, MyProtocol adında bir protokol tanımlanmış ve bir extension ile genişletilmiştir. Ancak, extension yalnızca SomeClass adlı bir sınıf tarafından benimsendiğinde geçerlidir. SomeClass, MyProtocol'ü benimsemektedir ve genişleme, someMethod() adlı bir özel uygulama sağlar. Diğer yandan, SomeStruct adlı bir yapı, MyProtocol'ü benimsemesine rağmen genişleme kısıtlamalarını karşılamadığından varsayılan bir someMethod() uygulaması kullanılır.





 



