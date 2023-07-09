## Access Control

OOP Temellerinden biri olan Encaupsulation, bir nesnenin içindeki verilerin ve fonksiyonların dışarıdan erişilebilir olmasını engelleyen bir kavramdır. Bu kavramın uygulanması için de erişim belirleyicileri kullanılır. Erişim belirleyicileri, bir nesnenin içindeki verilerin ve fonksiyonların dışarıdan erişilebilir olmasını engeller. Bu belirleyiciler, nesnenin içindeki verilerin ve fonksiyonların hangi durumlarda dışarıdan erişilebilir olacağını belirler. Bu başlık altında da Swift dilinde bulunan erişim belirleyicileri incelenecektir.

- Bir fonksiyonun geri dönüş değerinin access level'i, fonksiyonun access level'inden daha düşük olamaz.

- Bir public değişken dosyaya file-private veya private ile işaretlenemez. 


## Access Levels

Swift 5 farklı access level sunar. Bu access level'ler şunlardır:

- Open : En geniş erişim belirleyicisidir. Yalnızca class'lar ve class member'lar ile kullanılabilir. Open erişim belirleyicisine sahip bir class, başka bir modül içindeki class'lar tarafından miras alınabilir. Aynı zamanda open erişim belirleyicisine sahip bir class'ın member'ları, başka bir modül içindeki class'lar tarafından override edilebilir.
- Public : İşlevi Open ile aynı olmakla beraber Open'dan farkı, başka bir modül içindeki sınıfların ve yapıların bu sınıf ve yapıları miras alamamasıdır.
- Internal : Sadece modül içinde erişilebilir. Dışarıdan erişilemez. Default access level'dir. Bir değişkenin veya fonksiyonun access level'i belirtilmediğinde internal olarak kabul edilir.
- File-private : Sadece tanımlandığı dosya içinde erişilebilir. Dışarıdan erişilemez. Belirli bir işlevsellik tüm dosya içinde kullanıldığında dışarıya gizlemek için kullanılır.
- Private : Sadece tanımlandığı scope içinde erişilebilir. Dışarıdan erişilemez. Belirli bir işlevsellik tüm scope içinde kullanıldığında dışarıya gizlemek için kullanılır.

```swift
public class SomePublicClass {}
internal class SomeInternalClass {}
fileprivate class SomeFilePrivateClass {}
private class SomePrivateClass {}


public var somePublicVariable = 0
internal let someInternalConstant = 0
fileprivate func someFilePrivateFunction() {}
private func somePrivateFunction() {}
```

## Kullanımlar ve Notlar

Eğer bir class, struct veya enum'un access level'i belirtilmişse içerisindeki member'ların access level'i değiştirilmediği sürece default olarak mevcut yapıdan gelir. Örneğin:

```swift
public class SomePublicClass {                  // explicitly public class
    public var somePublicProperty = 0            // explicitly public class member
    var someInternalProperty = 0                 // implicitly internal class member
    fileprivate func someFilePrivateMethod() {}  // explicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}


class SomeInternalClass {                       // implicitly internal class
    var someInternalProperty = 0                 // implicitly internal class member
    fileprivate func someFilePrivateMethod() {}  // explicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}


fileprivate class SomeFilePrivateClass {        // explicitly file-private class
    func someFilePrivateMethod() {}              // implicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}


private class SomePrivateClass {                // explicitly private class
    func somePrivateMethod() {}                  // implicitly private class member
}
```

Burada eğer bir inheritence varsa subclass'ın access level'i superclass'tan yüksek olamaz.

Access level'ler override edilebilir:

```swift
public class A {
    fileprivate func someMethod() {}
}


internal class B: A {
    override internal func someMethod() {}
}
```

Bir fonksiyon, döndürdüğü değerdeki erişim düzeyinin en düşük erişim düzeyine sahip olmalıdır:

```swift
func someFunction() -> (SomeInternalClass, SomePrivateClass) { // error: Function must be declared private or fileprivate because its result uses a private type
    
} 
```

Düzeltirsek:
    
```swift
private func someFunction() -> (SomeInternalClass, SomePrivateClass) {
        
}
```

Bir yapıdan instance üretirken, instance'ın access level'i, yapıdan daha düşük olamaz:

```swift
private var privateInstance = SomePrivateClass() // private tanımlanmazsa hata verir.
```

