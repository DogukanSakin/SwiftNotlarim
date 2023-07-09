## Delegation

Delegation tasarım deseni, nesneler arasındaki iletişimi kolaylaştıran ve yeniden kullanılabilirlik sağlayan bir yöntemdir. Delegation, bir nesnenin belirli görevlerini veya olaylarını başka bir nesneye devretmek için kullanılır. Bu desen, bir nesnenin başka bir nesne adına bazı görevleri yerine getirmesine izin verir.

Swift'te Delegation, iki temel bileşen üzerinde çalışır: delegator (temsilci) ve delegate (temsil eden). Delegator, görevlerini veya olaylarını temsil eden nesnedir. Delegate ise, bu görevleri gerçekleştirecek nesnedir. Delegator, delegate'e sahip olur ve ona belirli görevleri yerine getirmesi için yetki verir.

Delegation kullanmanın temel avantajlarından biri, nesneler arasındaki bağımlılığı azaltmasıdır. Delegator, görevlerini gerçekleştirmek için direkt olarak bir sınıfa bağlı olmak yerine, bu görevleri delegate'e devreder. Böylece, delegator ve delegate arasındaki ilişki gevşetilir ve daha esnek bir yapı oluşturulur. Bu da kodun bakımını ve yeniden kullanılabilirliğini artırır.

## Delegation Aşamaları

Protocol oluşturma: İlk adım, delegate'in uygulaması gereken yöntemleri tanımlayan bir protocol oluşturmaktır. Bu protocol, delegator ve delegate arasında bir anlaşma sağlar ve hangi yöntemlerin uygulanması gerektiğini belirtir.

```swift
protocol MyDelegate {
    func didSomething()
    func didReceiveData(data: Any)
}
```

Delegate tanımlama: Delegator sınıfında, bir delegate özelliği tanımlanmalıdır. Bu özellik, delegate'e sahip olmak için kullanılır. Delegate, yukarıda oluşturulan protocolü uygulayan bir nesne olmalıdır.

```swift
class MyDelegator {
    var delegate: MyDelegate?
    
    func performTask() {
        // Görevin gerçekleştirilmesi
        delegate?.didSomething()
    }
    
    func receiveData(data: Any) {
        // Veri alındığında delegate'e bildirme
        delegate?.didReceiveData(data: data)
    }
}
```

Delegate'i atama: Delegate'i belirlemek için delegator sınıfının bir örneğini oluşturmanız ve delegate özelliğine bir değer atamanız gerekmektedir. Bu değer, yukarıda oluşturulan protocolü uygulayan bir nesne olmalıdır.

```swift
class MyDelegateImplementation: MyDelegate {
    func didSomething() {
        // Görev tamamlandığında yapılacaklar
    }
    
    func didReceiveData(data: Any) {
        // Veri alındığında yapılacaklar
    }
}

let delegator = MyDelegator()
let delegateImplementation = MyDelegateImplementation()

delegator.delegate = delegateImplementation
```
