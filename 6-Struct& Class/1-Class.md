## Class

Oluşturma syntax'ı aşağıdaki gibidir.

```swift
class SomeClass {
    // class definition goes here
}
```

## Değişkenler İçin Bellek Yönetimi

- Weak = Weak olarak işaretlenmiş bir değişken bellekten kaldırılma konusunda önceliklidir.

Örnek:

```swift
weak var myWeakVar = SomeClass()
``` 

- Strong = Strong olarak işaretlenmiş bir değişken bellekten kaldırılma konusunda öncelikli değildir. Bellekte tutulmaya çalışılır. Strong yapmak için herhangi bir şey yazmaya gerek yok default olarak değişken tanımlandığında strong'tur.

Örnek:

```swift
var myStrongVar = SomeClass()
```
## Identity Operator

Class'lar referans tipli olduğu için bellekteki adresleriyle karşılaştırılır. Bu yüzden == operatörü yerine === operatörü kullanılır.

```swift
if someIdenticalPerson === anotherPerson {
    print("These two people are indeed the same person")
}
```

