## Macros

Swift'te doğrudan makroların kullanımı yoktur. Bunun yerine, derleme zamanında çalışan ifadeleri oluşturmak için derleme süresi önişlemcisi direktifleri kullanılır. Swift dilindeki önişlemci direktiflerinin kullanım amaçları şunlar olabilir:

Derleme Koşulları: Önişlemci direktifleri, belirli derleme koşullarına göre kodun derlenmesini yönlendirmek için kullanılabilir. Örneğin, farklı platformlar (iOS, macOS) için platforma özgü kod bloklarını belirlemek veya derleme seçeneklerine bağlı olarak farklı kod parçalarını derlemek için kullanılabilir.

Hata Ayıklama ve Test Amaçları: Önişlemci direktifleri, hata ayıklama veya test sırasında ek kod veya loglama işlevselliği eklemek için kullanılabilir. Örneğin, DEBUG koşulunda yalnızca hata ayıklama modunda çalışacak kod bloklarını belirlemek için kullanılabilir.

Özelleştirilmiş Derleme Seçenekleri: Önişlemci direktifleri, belirli derleme seçeneklerine veya sembollere bağlı olarak farklı kod parçalarını derlemek için kullanılabilir. Örneğin, belirli bir sembolün tanımlı olup olmadığına veya belirli derleme seçeneklerine bağlı olarak farklı özelliklerin açılıp kapatılmasını sağlayabilirsiniz. 

## Freestanding Macros

Freestanding macrolar için # operatörü kullanılır:

```swift
func myFunction() {
    print("Currently running \(#function)")
    #warning("Something's wrong")
}
```

Burada #function, #warning gibi önişlemci direktifleri freestanding makrolardır. Bu önişlemci direktifleri, derleme zamanında çalışan ifadeleri oluşturmak için kullanılır.

## Attachted Macros

Ekli macro'lar için @ operatörü kullanılır.

Örneğin bu kodu: 

```swift
struct SundaeToppings: OptionSet {
    let rawValue: Int
    static let nuts = SundaeToppings(rawValue: 1 << 0)
    static let cherry = SundaeToppings(rawValue: 1 << 1)
    static let fudge = SundaeToppings(rawValue: 1 << 2)
}
```

Bu şekilde yazabiliriz:

```swift
@OptionSet<Int>
struct SundaeToppings {
    private enum Options: Int {
        case nuts
        case cherry
        case fudge
    }
}
```

Bu sayede okunabilirliği arttırabiliriz. Buradaki @OptionSet Swift'in standart kütüphanesindeki OptionSet protokolünü uygulayan bir struct oluşturur. Bu macro listedeki case'leri okur ve onlardan constant'lar oluşturur.

## Macro Yazıldığında Compiler'ın Davranışı

Swift macro'ları şu şekilde genişletir:

- Compiler kodu okur ve memory içerisinde bir macro temsilcisi oluşturur.
- Compiler bellekteki temsilin bir kısmını makroya gönderir. Bu işlem makroyu genişletir.
- Compiler makro çağırısını genişletilmiş haliyle değiştirir.
- Genişletilmiş makro kullanılarak derleme devam eder.

