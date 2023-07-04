## Initilazer Delegation

Initializer delegation, bir class'ın veya struct'ın başka bir initializer'ı kullanarak kendi başlatıcılarını çağırma işlemidir. Bu konsept, tekrarlayan kodu önlemek ve kodun daha temiz ve sürdürülebilir olmasını sağlamak için kullanılır.

Örneğin:

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

Yukarıdaki örnekte, "Person" adında bir sınıf tanımlanmıştır. Sınıfın iki farklı başlatıcısı bulunmaktadır. İlk başlatıcı, "name" ve "age" adında iki parametre alır ve bu parametrelerle sınıfın özelliklerini başlatır. İkinci başlatıcı ise sadece "name" parametresini alır ve "age" parametresini varsayılan değeri olan 0 ile başlatmak için ilk başlatıcıyı çağırır. Bu durumda, ikinci başlatıcıda "convenience" anahtar kelimesi kullanılmıştır.

"convenience" anahtar kelimesi, bir başlatıcının diğer bir başlatıcıyı çağırması durumunda kullanılır. İlgili başlatıcıya "convenience" anahtar kelimesi eklemek, başlatıcının kendi sınıfının tüm özelliklerini başlatmasına gerek olmadığını belirtir. Bunun yerine, başka bir başlatıcıyı çağırabilir ve sadece belirli parametreleri ayarlayabilir.

## Value Type'ta Initilazer Delegation

Struct value type olduğu için initializer delegation farklı bir şekilde çalışır. Value type olan yapılar, başka bir başlatıcıyı doğrudan çağıramazlar. Bunun yerine, kendi içlerinde başka bir başlatıcıyı çağırmak yerine, varsayılan değerlerle başlatılmış bir örneğe değer atayarak veya mevcut bir örneğin değerlerini kopyalayarak başlatılırlar.

```swift
struct Person {
    let name: String
    let age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    init(name: String) {
        self.init(name: name, age: 0)
    }
}
```
Bu şekilde, value type olan yapılar için initializer delegation, kendisini varsayılan değerlerle başlatılmış bir örneğe atayarak veya mevcut bir örneğin değerlerini kopyalayarak gerçekleştirilir.
