## Concurrency

Bu başlık altında Swift'in asenkron programlama için sunduğu özellikleri inceleyeceğiz.

Bir asenkron fonksiyonu tanımlamak için `async` anahtar kelimesini kullanabiliriz:

```swift
func fetchUser() async -> User {
    // ...
}
```

Birden fazla async fonksiyon oluşturur ve çağırırsak hepsi sırasıyla birer birer çalışacaktır.

Toplu async fonksiyonu çağırmak için şöyle bir kısa yol izlenebilir:
    
```swift
async let firstPhoto = downloadPhoto(named: photoNames[0])
async let secondPhoto = downloadPhoto(named: photoNames[1])
async let thirdPhoto = downloadPhoto(named: photoNames[2])


let photos = await [firstPhoto, secondPhoto, thirdPhoto]
show(photos)
 ```

Fonksiyonu çağırırken işlem tamamlanana kadar beklemek için `await` anahtar kelimesini kullanabiliriz:

```swift
let user = await fetchUser()
```





