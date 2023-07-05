## Error Handling

Swift, program runtime'ı boyunca oluşabilecek hataları yakalamak için, hata işleme mekanizması sunar. Bir hata oluştuğunda, programın çalışması durur ve hata yakalama mekanizması, hata ile ilgili bilgileri yakalar ve hata ile ilgili bilgileri, programın başka bir yerinde hata ile ilgili işlem yapmak için kullanılabilir.

Karşılaşabilinecek hataları enum'lar ile modelleyebiliriz:

```swift
enum LoginError: Error {
    case wrongUsername
    case wrongPassword
}
```

Hata fırlatmak için `throw` anahtar kelimesini kullanabiliriz:

```swift
func login(username: String, password: String) throws {
    if username != "admin" {
        throw LoginError.wrongUsername
    }
    
    if password != "1234" {
        throw LoginError.wrongPassword
    }
}
```

Swift'te error handling için 4 yol vardır:

- `do-catch` blokları
- `try?` ile optional dönüş değeri
- `try!` ile forced dönüş değeri
- `defer` blokları

Bir fonksiyonun hata fırlatabileceğini belirtmek için tanımlama:

```swift
func login(username: String, password: String) throws {
    // ...
}
```

Buradaki throws anahtar kelimesi return değerinden önce yazılır bir değer return ettiğimizde fonksiyon böyle gözükecek:

```swift
func login(username: String, password: String) throws -> Bool {
    // ...
}
```

### do-catch

`do-catch` blokları ile hata fırlatıldığında yakalayabiliriz:

```swift
do {
    try login(username: "admin", password: "1234")
    print("Login success")
} catch LoginError.wrongUsername {
    print("Wrong username")
} catch LoginError.wrongPassword {
    print("Wrong password")
} catch {
    print("Unknown error")
}
```

### try?

`try?` ile hata fırlatıldığında optional bir değer döner:

```swift
let loginResult = try? login(username: "admin", password: "1234")
```

### try!

`try!` ile hata fırlatıldığında forced bir değer döner:

```swift
let loginResult = try! login(username: "admin", password: "1234")
```

### defer

`defer` blokları, fonksiyonun sonunda çalıştırılacak kod bloklarıdır. Hata fırlatılsa bile çalıştırılır:

```swift
func login(username: String, password: String) throws {
    defer {
        print("Login finished")
    }
    
    if username != "admin" {
        throw LoginError.wrongUsername
    }
    
    if password != "1234" {
        throw LoginError.wrongPassword
    }
    
    print("Login success")
}
```


