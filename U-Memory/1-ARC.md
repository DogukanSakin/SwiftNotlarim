## Automatic Reference Counting (ARC)

Swift ARC'yi kullanarak hafızayı otomatik olarak yönetir. ARC, bir sınıf örneğine kaç referans olduğunu takip eder. Bir sınıf örneğine referans sayısı 0 olduğunda, ARC, sınıf örneğini hafızadan siler. ARC Yalnızca class'ları ve instance'ları yönetir. Struct'lar ve enum'ları değil. Çünkü bunlar değer türleridir.

## Nasıl Çalışır?

Class'tan bir instance oluşturduğumuz her zaman ARC bu instance ile ilgili bilgileri depolamak için bir bellek ayırır. Bu bellek, instance'ın türüyle ilgili bilgileri ve bu instance ile ilişkilendirilmiş property'lerin değerlerini tutar. Bu instance'a ihtiyaç kalmadığı durumda ARC, bu belleği serbest bırakır. Bu sayede bellek kullanımı optimize edilir. ARC bir instance'ın gerekli olup olmadığını belirlemek için instance'a kaç referans olduğunu takip eder. Bu referans sayısı, instance'a yeni bir referans oluşturulduğunda 1 artar. Bir referansın scope'u dışına çıktığında 1 azalır. Bir instance'a referans sayısı 0 olduğunda ARC, instance'ı hafızadan siler. 


Örneğin:

```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}

var reference1: Person?
var reference2: Person?
var reference3: Person?

reference1 = Person(name: "John Appleseed")
// Prints "John Appleseed is being initialized"

reference2 = reference1
reference3 = reference1

reference1 = nil
reference2 = nil
reference3 = nil // Tam bu satırda, Person instance'ı hafızadan silinir.
```

## Strong Reference Cycles

ARC'nin hiçbir zaman hafızayı serbest bırakamadığı durumlar vardır. Bu durumlara Strong Reference Cycles denir. Strong Reference Cycles, iki class instance'ı arasında oluşan bir ilişkidir. Bu ilişki, her iki instance'ın da birbirine strong reference oluşturmasıyla oluşur. Bu durumda ARC, bu iki instance'ı hafızadan silmez. Bu durumda ARC'nin hafızayı serbest bırakabilmesi için, bu iki instance'ın birbirine strong reference oluşturmasını engellememiz gerekir.

Bu durum aşağıdaki koşulda oluşur:

```swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment? 
    deinit { print("\(name) is being deinitialized") }
}


class Apartment {
    let unit: String
    init(unit: String) { self.unit = unit }
    var tenant: Person? 
    deinit { print("Apartment \(unit) is being deinitialized") }
}

var john: Person?
var unit4A: Apartment?

john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")

john!.apartment = unit4A //Linklendi, Strong Reference Cycle
unit4A!.tenant = john //Linklendi, Strong Reference Cycle

john = nil
unit4A = nil
```

Yukarıdaki örnekte en son aşamada instance'ları nil yaptığımızda, ARC bu instance'ları hafızadan silmez. Çünkü bu instance'lar birbirine strong reference oluşturmuştur. Bu durumda ARC'nin hafızayı serbest bırakabilmesi için, bu iki instance'ın birbirine strong reference oluşturmasını engellememiz gerekir. Çözüm için iki yol vardır. Weak ve Unowned Reference'lar. Burada bir instance'ın ömrü diğerine göre daha kısaysa Weak Reference, ömrü daha uzunsa Unowned Reference kullanılır.

## Weak Reference

Weak Reference, instance'ı hafızada kalıp kalmadığını kontrol etmez ve instance bellekten silindiğinde otomatik olarak nil değeri alır. Weak referance için weak keyword'ünü kullanırız. Weak referance'lar her zaman optional'dır. Çünkü instance'ın hafızada kalıp kalmadığını kontrol etmez. Bu yüzden weak referance'lar her zaman optional'dır.

```swift
class Person {
    let name: String
    weak var friend: Person?
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) deallocated")
    }
}

var john: Person? = Person(name: "John")
var jane: Person? = Person(name: "Jane")

john?.friend = jane
jane?.friend = john

john = nil
jane = nil
```

## Unowned Reference

Unowned Reference, weak reference'tan farklı olarak nil değerini almadan bir referansın varlığını garanti eder ve bir referansın her zaman geçerli olduğunu varsayar. Bu referans türü, bir nesnenin ömrü boyunca sürekli olarak var olması gerektiği durumlarda kullanılır.

```swift
class Person {
    let name: String
    unowned let bestFriend: Person
    
    init(name: String, bestFriend: Person) {
        self.name = name
        self.bestFriend = bestFriend
    }
    
    deinit {
        print("\(name) deallocated")
    }
}

var john: Person? = Person(name: "John", bestFriend: Person(name: "Jane", bestFriend: nil))
var jane: Person? = john?.bestFriend

john = nil
jane = nil
```

Unowned referanslar, referansların yaşam döngüsünün birbirine bağlı olduğu durumlarda kullanılır. Bellek yönetimi açısından weak'lerden farklıdır ve kullanırken dikkatli olunmalıdır. Eğer unowned bir referansın işaret ettiği instance bellekten silinirse, hata oluşabilir. Bu nedenle, kullanmadan önce referansın sürekli olarak geçerli olacağından emin olunmalıdır.

## Strong Reference Cycles for Closures 

Bir clouser içinde başka bir instance'a referans oluşturulduğunda ve bu instance'da clouser'a string bir şekilde referans oluşturduğunda strong reference cycle oluşur. Bu durumda, instance'lar birbirlerini hatırlar ve bellekte kalır, bu da hafıza sızıntısına yol açar.

```swift
class Person {
    var name: String
    lazy var introduce: () -> String = {
        return "My name is \(self.name)"
    }
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) deallocated")
    }
}

var john: Person? = Person(name: "John")
print(john?.introduce() ?? "") // "My name is John"

john = nil
```

Yukarıdaki örnekte, Person adında bir class tanımlanmıştır. Bu class'ın name adında bir property'si ve introduce adında bir clouser'ı bulunur. Clouser, kendi adını ve name özelliğini kullanarak bir string döndürür.

Person class'ının introduce clouser'ı, self keyword'üyle Person örneğine erişir. Bu durumda, clouser Person örneğine strong bir şekilde bağlıdır.

Örnekte, john adında bir Person instance'ı oluşturulur ve introduce clouser'ı çağrılır. Bu durumda, clouser self.name ifadesine  strong reference cycle oluşturarak john instance'ını hatırlar.

Sonrasında john değişkeni nil olarak atanır. Bu durumda, referans sayısı sıfıra düştüğünde Person örneği bellekten otomatik olarak silinir.

deinit metodu, bir instance bellekten silindiğinde çağrılır. Bu örnekte, deinit metodu çağrıldığında, silinen örneğin adını ekrana yazdırır.

Bu örnekte, clouser içindeki self ifadesi,  strong reference cycle'a neden olan bir referansa dönüşür. Bu tür bir durumda, bellek sızıntısı meydana gelebilir ve instance'ların beklenmedik bir şekilde bellekte kalmasına neden olabilir.

Strong reference cycle durumunu önlemek için, weak veya unowned referansları kullanabiliriz. Bu, clouser'ın kendi içindeki self referansını string bir şekilde tutmamasını sağlar ve bellek sızıntısını önler.

```swift
class Person {
    var name: String
    lazy var introduce: () -> String = { [weak self] in
        guard let self = self else {
            return "Person is deallocated"
        }
        return "My name is \(self.name)"
    }
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) deallocated")
    }
}

var john: Person? = Person(name: "John")
print(john?.introduce() ?? "") // "My name is John"

john = nil
```

introduce clouser'ı [weak self] ifadesi kullanılarak güncellenmiştir. Bu sayede clouser içinde self için zayıf bir referans oluşturulur. guard let ifadesi kullanılarak, clouser'ın çalışma zamanında self referansının nil olup olmadığı kontrol edilir. Eğer self nil ise, "Person is deallocated" mesajı döndürülür. Aksi takdirde, self güçlü hale getirilerek kullanılır ve clouser'ın çalışması devam eder.

Bu değişiklik, clouser'ın kendisine güçlü bir şekilde referans oluşturmaktan kaçınarak referans döngüsünü önler ve bellek sızıntısını çözer. Artık Person örneği bellekten silindiğinde, introduce clouser'ı nil değeri döndürerek doğru bir mesaj döndürür ve bellek sızıntısı oluşmaz.

Bu şekilde, weak referans kullanarak güçlü referans döngülerini çözebiliriz ve bellek yönetimini daha etkin hale getirebiliriz.






