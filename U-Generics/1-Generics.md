## Generics

Generic fonksiyonlar Swift'in oldukça güçlü yönlerinden biridir. Türe bağlı olmadan çalışan fonksiyonlar yazmamızı sağlar. Bu sayede kod tekrarını önler ve daha az hata yapmamızı sağlar.

Örneğin integer için toplama yapmayı hedeflediğimiz bir fonksiyonumuz olsun:

```swift
func addIntegers(x: Int, y: Int) -> Int {
    return x + y
}
```

Daha sonra Double için de bunu yapmak istediğimizi düşünelim. Benzer şekilde Float için de. Böyle böyle kod satırlarımız her tür için artacak ve aynı işlemi kopylayacağız. İşte tam olarak generic yapılar bu sorunu çözer. Bu toplama fonksiyonunu generic fonksiyon olarak yazmak istersek:

```swift
func add<T>(x: T, y: T) -> T {
    return x + y
}
```
Bu şekilde integer,double, float,string vs. tüm türler için ortak çalışan bir fonksiyon yazmış olduk. 

Burada generic fonkisyon oluştururken paramtere isimleri için normalde aralarında eğer bir ilişki olan türlerin isimlendirilmesi doğrudan anlaşılır yazılmalıdır. Örneğin: Dictionary<Key, Value> gibi.

Ancak yukarıdaki örnekte olduğu gibi doğrudan bir fonksiyon aralarında bir ilişki olmayan türler için kullanılacağından ötürü T, U, V gibi isimler kullanılabilir. Ayrıca burada upper camel case kullanılması da önemlidir.

## Extension ve Generics

Extensionlar generic türler için de kullanılabilir. Örneğin:

```swift
extension Array {
    func randomItem() -> Element? {
        if isEmpty { return nil }
        let index = Int(arc4random_uniform(UInt32(self.count)))
        return self[index]
    }
}
```

Burada Element generic türdür ve array içindeki öğeleri temsil etmek için kullanılır. Bu tür standart olarak gelir.

## Generic Subscripts

Generic türler için subscript'ler de kullanılabilir. Örneğin:

```swift
extension Array {
    subscript<Indices: Sequence>(indices: Indices) -> [Element] where Indices.Iterator.Element == Int {
        var result = [Element]()
        for index in indices {
            result.append(self[index])
        }
        return result
    }
}
```

## Type Constraints

Generic fonksiyonlar için tür kısıtlamaları getirilebilir. Örneğin:

```swift
func add<T: Numeric>(x: T, y: T) -> T {
    return x + y
}
```

Burada T türü Numeric protokolünü uygulayan türlerden biri olmalıdır. Bu sayede sadece sayısal türler için çalışan bir fonksiyon yazmış olduk.

## associatedtype

Protokollerde de generic türler kullanılabilir. Örneğin:

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

## Generic ve Where

Generic fonksiyonlarda where kullanarak tür kısıtlamaları getirebiliriz. Örneğin:

```swift
func add<T>(x: T, y: T) -> T where T: Numeric {
    return x + y
}
```

Benzer şekilde extension'lar için de where kullanılabilir. Örneğin:

```swift
extension Array where Element: Numeric {
    func sum() -> Element {
        return reduce(0, +)
    }
}
```

Benzer şekilde protocol'de tanımladığımız associatedtype için de where kullanılabilir. Örneğin:

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
    func sum() -> Item where Item: Numeric
}
```

