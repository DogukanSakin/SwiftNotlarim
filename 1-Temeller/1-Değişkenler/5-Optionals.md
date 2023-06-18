## Optionals

Nullable ifadesi olarakta değerlendirilen bu ifade özetle bir değişken için bellekte bulunabilirde bulunmayabilirde demenin yoludur.

Örneğin "abc" stringini bir int'e çevirmeye çalıştığımızda program doğal olarak çöker. Bu çökmeyi önlemenin yolu optionals'dan geçer.

Örneğin

```
var age : Int
```

Tanımlamasını yaptığımızı düşünelim. Burada age'i print etmek istesek initilaze olmadığı için hata alacağız ancak değişkeni optional yaparsak

```
var age : Int?
```

Ve bu halde print etmek istersek nil sonucunu görürüz. Bu kullanımda herhangi bir değer ataması yapmazsak değişkene otomatik olarak nil atanır.

Optional bir değeri derleyiciye nil gelmeyeceğini garanti etmek için ! kullanılır.

```
print(age!)
```

Ancak bu durum risklidir. Eğer age'e bir değer ataması yapılmazsa kod çöker.

## ! ve ? işaretleri için ayrıntı:

Swift programlama dilinde, ? ve ! operatörleri, değişkenlerin veya nesnelerin opsiyonel (optional) türleriyle çalışırken kullanılır. Bu operatörler, Swift'in opsiyonel değerleri işleme biçimini belirler.

? Operatörü (Opsiyonel Zincirleme Operatörü):

- Bir değişkenin veya nesnenin opsiyonel bir değere sahip olup olmadığını kontrol etmek için kullanılır.
- Eğer opsiyonel değer nil ise, ? operatörü sonucu nil olarak döndürür.
- Eğer opsiyonel değer nil değilse, ? operatörü sonraki işleme geçer.
- ? operatörü, bir zincirleme yapısı içinde birden fazla kullanılabilir.
- Örneğin: myOptionalVariable?.property

! Operatörü (Zorunlu Çözme Operatörü):

- Bir değişkenin veya nesnenin opsiyonel değerini zorunlu olarak çözmek (unwrap) için kullanılır.
- Eğer opsiyonel değer nil ise, ! operatörü hata verir (runtime hatası) ve program çalışmayı durdurur. Eğer opsiyonel değer nil değilse, ! operatörü opsiyonel değeri zorunlu değere dönüştürür.
- ! operatörü, opsiyonel değerin kesinlikle nil olmadığı durumlar için kullanılmalıdır.

Örneğin: myOptionalVariable!

? ve ! operatörleri, opsiyonel değerleri güvenli bir şekilde kontrol etmek ve kullanmak için kullanılır. Özellikle, bir değişkenin nil olma durumunu kontrol etmek istediğinizde ? operatörünü, değişkenin kesinlikle nil olmadığını bildiğiniz durumlarda ise ! operatörünü kullanabilirsiniz. Ancak ! operatörünü dikkatli bir şekilde kullanmalı ve opsiyonel değerlerin nil olma durumunu önceden kontrol etmek için ? operatörünü kullanmanız önerilir. Bu, programınızda beklenmedik hataları önlemeye yardımcı olur.