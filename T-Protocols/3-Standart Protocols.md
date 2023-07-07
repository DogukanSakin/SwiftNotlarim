## Standart Protocols

Swift'te, bir tipin bir protocol'e uyum sağlaması durumunda, belirli durumlarda uyum sağlayan kodun otomatik olarak oluşturulmasını sağlar. Bu özellik, protocol'ün gerektirdiği tüm özellikleri sağlayan varsayılan uygulamaların oluşturulmasıyla tipin protocol'e uyum sağlamasını kolaylaştırır. Protokolün bazı gereklilikleri, tipin kendi içerisinde uygulanabilirken, diğer gereklilikler otomatik olarak oluşturulan varsayılan bir uygulama ile sağlanabilir. Böylece, tekrarlayan veya basit uygulamaları tekrar yazma ihtiyacı ortadan kalkar ve kodun daha az tekrarlanması ve daha sade olması sağlanır.

Swift'in sağladığı otomatik olarak eklenen protocol'ler:

- Equatable
- Hashable
- Comparable
- Error

## Equatable

Equatable protokolü, bir tipin eşitlik karşılaştırmasını gerçekleştirmesini sağlar. Bu protokolü benimseyen bir tip, == operatörünü kullanarak başka bir aynı tipteki değerle karşılaştırılabilir. Equatable protokolü, örneğin iki dizeyi veya iki sayıyı karşılaştırmak için kullanılabilir.

```swift
struct Person: Equatable {
    var name: String
    var age: Int
}

let person1 = Person(name: "Alice", age: 25)
let person2 = Person(name: "Bob", age: 30)

if person1 == person2 {
    print("Person1 and Person2 are equal")
} else {
    print("Person1 and Person2 are not equal")
}
```

## Hashable

Hashable protokolü, bir tipin karma işlevini uygulamasını sağlar. Karma işlevi, bir değeri benzersiz bir sayısal değere dönüştürür. Hashable protokolü, bir tipin eşitlik karşılaştırmasının yanı sıra, veri yapıları gibi hash tablolarında veya kümeleme yapısında kullanılabilmesini sağlar.

```swift
struct Person: Hashable {
    var name: String
    var age: Int
}

let person = Person(name: "Alice", age: 25)
let hashValue = person.hashValue
```

## Comparable

Comparable protokolü, bir tipin karşılaştırılabilirlik işlevini sağlar. Bu protokolü benimseyen bir tip, <, <=, >, >= operatörlerini kullanarak başka bir aynı tipteki değerle karşılaştırılabilir. Comparable protokolü, sıralama gerektiren veri yapılarında veya algoritmalarında kullanılabilir.

```swift
struct Person: Comparable {
    var name: String
    var age: Int
}

let person1 = Person(name: "Alice", age: 25)
let person2 = Person(name: "Bob", age: 30)

if person1 < person2 {
    print("Person1 is younger than Person2")
} else if person1 > person2 {
    print("Person1 is older than Person2")
} else {
    print("Person1 and Person2 have the same age")
}
```

## Error

Error protokolü, bir hata durumunu temsil etmek için kullanılır. Bir hata durumu oluştuğunda, hata fırlatılabilir (throw) ve Error protokolünü benimseyen bir türle temsil edilebilir. Hata fırlatma ve hata yakalama mekanizması, Swift'teki hata yönetimi için kullanılır.

```swift
enum NetworkError: Error {
    case invalidURL
    case serverError
    case authenticationError
}

func fetchData(from url: String) throws {
    guard let validURL = URL(string: url) else {
        throw NetworkError.invalidURL
    }
}

do {
    try fetchData(from: "https://example.com")
} catch let error {
    print("Error occurred: \(error)")
}
```







