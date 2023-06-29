## Guard

Swift programlama dilinde "guard" ifadesi, bir koşulu kontrol etmek ve koşulun sağlanmadığı durumlarda erken çıkış yapmak için kullanılan bir kontrol akışı ifadesidir. Guard ifadesi, özellikle fonksiyonların başında, değerlerin geçerliliğini kontrol etmek için yaygın olarak kullanılır.

Guard ifadesi, bir koşulu değerlendirir ve koşulun sağlanmadığı durumlarda else bloğundaki kodu çalıştırır. Bu, fonksiyonun devam etmesini veya geri dönmesini engeller.

Guard ifadesi, aynı zamanda değerleri bir opsiyonel bağlamadan çıkarmak veya unwrap yapmak için de kullanılabilir. Bir değerin nil olup olmadığını kontrol eder ve nil ise else bloğundaki kodu çalıştırır.

```swift
func processUser(username: String?, age: Int?) {
    guard let username = username else {
        print("Kullanıcı adı geçersiz.")
        return
    }

    guard let age = age, age >= 18 else {
        print("Yaş geçersiz veya yaş sınırı tutmuyor.")
        return
    }

    // Koşullar sağlandı, devam eden kodlar...
    print("Kullanıcı adı: \(username), yaş: \(age)")
}

processUser(username: "john", age: 25)
```

## If'ten Farkı

Guard ifadesi ve if ifadesi, Swift'te kontrol akışı için kullanılan iki farklı ifadedir. İkisi de koşulları değerlendirir ve koşulun sağlanıp sağlanmadığını kontrol eder, ancak çalışma şekilleri ve amaçları açısından farklılık gösterirler.

İşte guard ifadesi ve if ifadesi arasındaki farklar:

- Erken Çıkış: Guard ifadesi, koşulun sağlanmadığı durumlarda erken çıkış yapar. Else bloğunda yer alan kod çalışır ve fonksiyondan, döngüden veya kod bloğundan çıkılır. Bu, kodun okunabilirliğini artırır ve beklenmeyen durumları erken tespit etmeye yardımcı olur. If ifadesi ise, koşulun sağlanmadığı durumda else bloğu çalışır, ancak else bloğundan sonra kodun devam etmesine izin verir.

- Değeri Unwrap Etme: Guard ifadesi, bir opsiyonel değeri unwrap etmek veya çıkarım yapmak için sıklıkla kullanılır. Eğer unwrap işlemi başarısız olursa, else bloğundaki kod çalışır ve erken çıkış yapılır. If ifadesi ise, değeri unwrap etmek için kullanılan "?" veya "!" operatörlerini kullanır, ancak unwrap işlemi başarısız olduğunda hata alır ve else bloğuna geçmez.

- Scoping: Guard ifadesi, geçerli bir kapsam (scope) içinde çalışır. Değişkenlerin veya sabitlerin değerlerini guard ifadesi içerisinde unwrap ettikten sonra, bu değerler kapsamın geri kalanında kullanılabilir. If ifadesi ise, değişkenlerin veya sabitlerin değerlerini sadece if bloğu içinde kullanır ve if bloğundan sonra bu değerlere erişim sağlanmaz.