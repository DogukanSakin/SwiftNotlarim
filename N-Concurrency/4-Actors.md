## Actors

Actors, eşzamanlılık ve paralellik sorunlarını ele almak için kullanılan bir modeldir. Actors, paylaşılan durumun güvenli bir şekilde kullanılmasını sağlar ve aynı anda yalnızca bir iş parçacığı tarafından erişilebilirler. 

Actors, belirli bir kapsamda tanımlanan ve birincil iş parçacığı dışında hiçbir iş parçacığı tarafından doğrudan erişilemeyen özel nesnelerdir. Actors, diğer iş parçacıklarıyla iletişim kurmak için mesajlaşma yoluyla etkileşimde bulunurlar. Yani, bir aktöre mesaj gönderildiğinde, aktör bu mesajı alır, işler ve gerekirse yanıt döndürür.

```swift
actor Counter {
    private var count = 0
    
    func increment() {
        count += 1
    }
    
    func getCount() -> Int {
        return count
    }
}
```

Bu örnekte, Counter adında bir aktör tanımlanmıştır. count adında özel bir değişken ve increment ve getCount adında iki metot bulunmaktadır. count değişkeni, aktör içinde paylaşılan durumu temsil eder ve yalnızca aktörün kendi iş parçacığı tarafından güncellenebilir.

Actors, bir actore ait metotlara erişmek için await ifadesiyle mesaj gönderme yöntemini kullanırız.

```swift
Task {
    let counter = Counter()
    await counter.increment()
    let count = await counter.getCount()
    print(count) // Output: 1
}
```

Actors, paylaşılan durumu güvenli bir şekilde yönetmeyi sağlar ve eşzamanlı çalışma ortamında hatalara ve yarış koşullarına karşı koruma sağlar. Aynı anda yalnızca bir iş parçacığı tarafından erişilebilen actors, paralel işleme ihtiyacı duyan uygulamalar için önemli bir araçtır.

Actors referans tiplidir. Dolayısıyla class gibi kullanılabilirler:

```swift
actor TemperatureLogger {
    let label: String
    var measurements: [Int]
    private(set) var max: Int


    init(label: String, measurement: Int) {
        self.label = label
        self.measurements = [measurement]
        self.max = measurement
    }
}
```

class'lardan farklı olarak aynı anda yalnızca bir iş parçacığı tarafından erişilebilirler. Dolayısıyla, actors'lerin paylaşılan durumu güvenli bir şekilde yönetmesi sağlanır.