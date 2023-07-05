## Unstructured Concurrency

Swift 5.5 ile birlikte, Unstructured Concurrency adı verilen yeni bir özellik eklendi. Bu özellik, geliştiricilere daha esnek ve ifade odaklı bir şekilde eşzamanlı işlemler gerçekleştirme imkanı sunar. Yapısal olmayan eşzamanlılık, bir görevin başka görevleri başlatması ve yönetmesi için kullanılır.

```swift
func performTasksConcurrently() async {
    await withTaskGroup(of: Void.self) { group in
        group.addTask {
            await Task.sleep(1_000_000_000) // 1 saniye bekle
            print("Görev 1 tamamlandı")
        }
        
        group.addTask {
            await Task.sleep(2_000_000_000) // 2 saniye bekle
            print("Görev 2 tamamlandı")
        }
    }
    
    print("Tüm görevler tamamlandı")
}

Task {
    await performTasksConcurrently()
}

```

## Task

Task anahtar kelimesi, Swift dilinde asenkron işlemleri temsil etmek için kullanılan bir yapıdır. Swift 5.5 ve sonraki sürümlerde yer almaktadır. Task anahtar kelimesi, asenkron işlemleri oluşturmak, başlatmak ve yönetmek için kullanılır.

Bir Task nesnesi, bir görevin temsilidir ve bağımsız bir çalışma birimidir. Bu görev, yanlızca bir kere çalıştırılabilir ve tamamlandığında sonlanır. Task yapısı, iş parçacıklarında veya dispatçı kuyruklarında çalışabilen eşzamanlı bir şekilde yürütülebilir.

Task yapısı, asenkron işlemleri oluşturmak için çeşitli yöntemlere sahiptir:

Task.detached yöntemi, bağımsız bir görevi başlatmak için kullanılır. Bu görev, anında başlar ve yürütülmesi için bir iş parçacığı veya dispatçı kuyruğu seçilir.

```swift
Task.detached {
    // Görevin yürütülmesi gereken kod
}
```

Task { } yapıcısı, await ifadesiyle birlikte kullanılarak bir görev oluşturur. Bu görev, çalıştırıldığında bir iş parçacığı veya dispatçı kuyruğunda yürütülür.

```swift
Task {
    // Görevin yürütülmesi gereken kod
}
```

Task(priority: .default) { } yapıcısı, önceliği belirtilmiş bir görev oluşturur. Öncelik, .userInitiated, .default, .utility veya .background gibi değerlerle belirtilebilir.


```swift
Task(priority: .default) {
    // Görevin yürütülmesi gereken kod
}
```
Task yapısı, asenkron işlemleri yürütmek ve yönetmek için çeşitli yöntemlere ve özelliklere sahiptir:

- await ifadesi, bir görevin tamamlanmasını beklemek için kullanılır.
- Task.sleep yöntemi, belirli bir süre boyunca görevin uyumasını sağlar.
- Task.isCancelled özelliği, görevin iptal edilip edilmediğini belirtir.
- Task.checkCancellation yöntemi, görevin iptal edilip edilmediğini kontrol eder ve gerekirse bir hata fırlatır.

Ayrıca, Task yapısı, görevler arasında veri paylaşımı ve senkronizasyon sağlamak için Task.LocalValues ve Task.Group gibi ilgili yapılarla da birlikte kullanılabilir.
