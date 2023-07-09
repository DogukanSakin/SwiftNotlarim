## Encapsulation

Encapsulation, bir class'ın veya yapıyı oluşturan verilerin ve işlevlerin nasıl gizlendiğini ve erişilebilir olduğunu kontrol etme yeteneğidir. Encapsulation, nesne yönelimli programlamanın temel prensiplerinden biridir ve kodun daha organize, anlaşılır ve bakımı kolay hale getirilmesini sağlar. Encapsulation şunları sağlar:

- Veri Gizliliği: Encapsulation, bir class'ın veya yapının içindeki verilerin gizlenmesini sağlar. Sadece class'ın kendisi bu verilere doğrudan erişebilir ve dışarıdan erişim engellenir. Bu, verilerin yanlışlıkla değiştirilmesini veya doğrudan erişimle hatalı manipülasyonlara neden olmasını önler.

- Arayüz Standardizasyonu: Class'ların veya yapıların nasıl kullanılacağına dair bir arayüz sağlamak encapsulation'ın bir parçasıdır. Class'ın veya yapının iç detaylarına odaklanmaktan ziyade, dışarıdaki kullanıcılar için erişilebilir işlevler ve özellikler sunulur. Bu, kullanıcıların class'ın iç yapısını bilmelerine gerek kalmadan, class'ın sunduğu özellikleri ve işlevleri kullanmalarını sağlar.

- Kodun Modüleritesi: Encapsulation, kodun modüler ve yeniden kullanılabilir olmasını sağlar. Bir class'ın veya yapının iç yapısında yapılan değişiklikler, dışarıya etki etmeden class'ın dış arayüzünü korur. Bu, kodun daha kolay bakımını sağlar ve bir bileşenin iç yapısında yapılan değişikliklerin diğer kod bölümlerini etkilemeden yapılabilmesini sağlar.

- Güvenlik: Encapsulation, class'ın veya yapının dışarıdaki kodlardan korunmasını sağlar. Class'ın iç detaylarının gizli kalması, kodun daha güvenli olmasını sağlar. Dışarıdaki kodlar sadece class'ın sunduğu arayüzü kullanarak etkileşimde bulunabilir ve iç detaylara erişemez.

- Kodun Anlaşılabilirliği: Encapsulation, kodun daha anlaşılabilir olmasını sağlar. Bir class veya yapı, sadece ilgili işlevlerin ve özelliklerin bir arada olduğu birim olarak düşünülür. Bu, kodun daha okunaklı, anlaşılır ve bakımı kolay hale gelmesini sağlar.


Encapsulation temelde getter ve setter'lar ile yapılır: 

```swift
var myVar: String {
    get {
        return "Hello" // Burada değişkenin kendisini sonsuz döngü oluşmaması için kullanmamalıyız.
    }
    set (newValue) {
        print(newValue)
    }
}
```

Eğer yalnızca get yazılırsa değişkene hiçbir şekilde atama yapamayız. Benzer şekilde setlersek okuyamayız.
