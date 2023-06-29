## Defer

"defer" ifadesi, bir kod bloğunun, belirli bir kapsamdan çıkış yapmadan hemen önce çalıştırılmasını sağlayan bir yapıdır. Defer ifadesi, genellikle kaynakların temizlenmesi, dosyaların kapatılması veya geçici durumların sıfırlanması gibi işlemleri gerçekleştirmek için kullanılır.

Defer ifadesi, bir blok içindeki kodun sona erdiği noktada veya kapsamdan çıkış yapılacağı noktada çalıştırılır. Bu, fonksiyonun sonunda, döngünün tamamlanmasında veya bir kontrol akışı yapısının sonunda çalıştırılmasını sağlar. Defer ifadesi, kodun okunabilirliğini artırır ve kaynak yönetimi ve temizleme işlemlerini daha tutarlı ve hatasız hale getirir.

```swift
var score = 1
if score < 10 {
    defer {
        print(score)
    }
    score += 5
}
// Prints "6"
```

Bir kod bloğunda birden fazla defer varsa en son tanımlanan ilk çalışır.

```swift
if score < 10 {
    defer {
        print(score)
    }
    defer {
        print("The score is:")
    }
    score += 5
}
// Prints "The score is:"
// Prints "6"
```
