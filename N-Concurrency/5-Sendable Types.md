## Sendable Types

Swift 5.5 ile gelen bu özellik asenkron işlemler arasında güvenli bir şekilde veri paylaşımını sağlamak için kullanılan türlerdir.

Sendable türler, eşzamanlılık ve paralellik senaryolarında güvenli bir şekilde kullanılmak üzere tasarlanmıştır. Bu türler, farklı iş parçacıklarında eşzamanlı olarak çalışan asenkron işlemler arasında veri paylaşımını mümkün kılar.

Bir türün Sendable olarak işaretlenmesi, bu türün eşzamanlılık sorunlarına karşı güvenli olduğunu ve birden çok iş parçacığı tarafından aynı anda erişilebileceğini belirtir. Sendable türler, güvenli bir şekilde kopyalanabilen ve paylaşılabilen türlerdir.

Sendable bir tür oluşturmak için, türü Sendable protokolünü uygulayacak şekilde işaretlemeniz yeterlidir:

```swift
struct Point: Sendable {
    var x: Int
    var y: Int
}
```

Point yapısı Sendable protokolünü uyguladığı için Sendable olarak işaretlenmiştir. Artık bu Point yapısı, farklı iş parçacıkları arasında güvenli bir şekilde paylaşılabilir.

Sendable türler, genellikle asenkron işlemlerle birlikte kullanılan aktörler ve diğer eşzamanlılık özellikleriyle birlikte etkin olarak kullanılır. Örneğin, bir aktör içinde Sendable türler kullanarak verilerin güvenli bir şekilde paylaşılmasını sağlayabilirsiniz.