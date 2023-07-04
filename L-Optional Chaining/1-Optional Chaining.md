## Optional Chaining

Optional Chaining, bir değeri veya metodu zincirleme şeklinde güvenli bir şekilde kullanmanıza olanak sağlayan bir özelliktir. Bu özellik, birçok durumda nil değerlerle çalışırken güvenliğinizi sağlamak için kullanılır.

Optional Chaining'in temel fikri, bir değeri kullanmadan önce nil kontrolü yapmanıza gerek kalmadan değeri zincirleme şeklinde kontrol etmenizi sağlamaktır. Bu, nil değerlerle çalışırken sürekli nil kontrolü yapma ihtiyacını ortadan kaldırır ve kodunuzun daha temiz ve daha okunaklı olmasını sağlar.

Optional Chaining'i kullanarak bir değeri veya metodu zincirleme şeklinde erişmek için aşağıdaki syntax'ı kullanabilirsiniz:

```swift
optionalValue?.property
optionalValue?.method()
```