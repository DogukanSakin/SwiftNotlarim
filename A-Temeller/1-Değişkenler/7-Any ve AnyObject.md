## Any ve AnyObject

Any, Swift dilinde, herhangi bir türden değerleri temsil etmek için kullanılır. AnyObject, Swift dilinde, herhangi bir sınıf türünden değerleri temsil etmek için kullanılır. Any ve AnyObject, tür güvenliği olmayan kod yazmak için kullanılır. Bu nedenle, Any ve AnyObject kullanımından kaçınılmalıdır.

```swift
var anyValue: Any = 5
anyValue = "Hello, World!"
anyValue = true
```

```swift
var anyObjectValue: AnyObject = "Hello, World!"
anyObjectValue = 5
anyObjectValue = true
```
