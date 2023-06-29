## Touples

İçerisinde çok sayıda ve farklı türde verilerin tutulmasına yarayan data structure.

Kullanım:

```swift
var t1 = (12,14.6,"string",true)
```

Erişmek için:

```swift
t1.0 // 12'yi alır
```

Atamada yapabiliriz, uygun türde olması kaydıyla:

```swift
t1.0 = 13
```

Touple değerlerine isimde verebiliriz.

```swift
var t2 = (td1: 21, td2: "string")
```

Sonradan da isim verebiliriz:

```swift
let http404Error = (404, "Not Found")
let (statusCode, statusMessage) = http404Error
```

Eğer sadece birine ihtiyacımız varsa _ ile boşta geçebiliriz.

```swift
let (statusCode, _ ) = http404Error
```



