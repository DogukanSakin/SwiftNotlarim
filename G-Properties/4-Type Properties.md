## Type Properties

Swift'te "Type Properties" olarak adlandırılan özellikler, bir türün kendisine ait olan ve tüm örnekler arasında paylaşılan özelliklerdir. Bu özellikler, bir türün tek bir kopyasını tutar ve örneklere özgü olmayan değerler veya davranışlar sağlar.

Type Properties, bir türün kendisine ait olan ve tüm örnekler tarafından kullanılan sabit veya değişken özellikler olabilir. Bu özellikler, türün kendisine ait olduğu için doğrudan tür adı üzerinden erişilebilirler ve örneklere ait bir kopyaları olmadığından örneklere özgü değerler taşımazlar. static anahtar kelimesi ile tanımlanırlar.

```swift
struct MyStruct {
    static var myTypeProperty: Int = 10

    static func myTypeMethod() {
        print("This is a type method.")
    }
}

print(MyStruct.myTypeProperty) // 10
MyStruct.myTypeProperty = 20
print(MyStruct.myTypeProperty) // 20

MyStruct.myTypeMethod() // This is a type method
```

Burada tanımlama yaparken her zaman bir başlangıç değeri vermek zorundayız. Bunun nedeni, türün kendisinin, initialize zamanında depolanan tür özelliğine bir değer atayabilecek bir init'e sahip olmamasıdır. Saklanan tür özellikleri, ilk erişimlerinde lazy olarak başlatılır. Aynı anda birden fazla iş parçacığı tarafından erişildiğinde bile yalnızca bir kez başlatılmaları garanti edilir ve lazy modifier ile işaretlenmeleri gerekmez.

Ayrıca class anahtar kelimesi ile tanımlanan sınıflar için de type property tanımlanabilir. Bu durumda, type property'lerin varsayılan değeri static anahtar kelimesi ile tanımlanan type property'lerden farklıdır. class anahtar kelimesi ile tanımlanan type property'lerin varsayılan değeri override edilebilir.

```swift
class MyClass {
    class var myTypeProperty: Int {
        return 10
    }
}

print(MyClass.myTypeProperty) // 10
```