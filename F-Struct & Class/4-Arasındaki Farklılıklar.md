## Class ve Struct Arasındaki Farklılıklar

Class'lar referans tiplerdir ve Heap bölgesinde tutulur. Stack bölgesinde ise referanslar tutulur. Kod bloğunun dışına çıkıldığında stack'teki referans hemen bellekten düşüp uygun görüldüğünde heap bölgesindeki verisi de temizlenir. 

Struct'lar değer tiplerdir. Referans yapısı bulunmaz ve veri Stack'te tutulur. Kod bloğunun dışına çıkıldığında stack'teki veri hemen bellekten düşer.

Eğer her durumda veri bellekte tutulmadan doğrudan temizlenmesini istiyorsak Struct kullanabiliriz.

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person1 = Person(name: "John")

var person2 = person1

person1.name = "Jack"

print(person1.name) // Jack

print(person2.name) // Jack
```

```swift

struct Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person1 = Person(name: "John")

var person2 = person1

person1.name = "Jack"

print(person1.name) // Jack

print(person2.name) // John
```

Fonksiyonlara parametre gönderirken Class'lar referans olarak gönderilir. Struct'lar ise kopyalanarak gönderilir.

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

func changeName(person: Person) {
    person.name = "Jack"
}

var person = Person(name: "John")

changeName(person: person)

print(person.name) // Jack
```

```swift

struct Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

func changeName(person: Person) {
    var person = person
    person.name = "Jack"
}

var person = Person(name: "John")

changeName(person: person)

print(person.name) // John
```

Class oluştururken tanımladığımız değerler optional değilse init yazmak zorundayız. Struct'lar için bu zorunlu değildir.

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person = Person(name: "John")

print(person.name) // John
```

```swift

struct Person {
    var name: String
}

var person = Person(name: "John")

print(person.name) // John
```

Struct içerisinde tutulan verilere başlangıç değeri vermezsek instance oluştururken mutlaka değer vermek zorundayız. Class'ta bunu yapmak için parametreli init yazmak zorundayız.

```swift

struct Person {
    var name: String
}

var person = Person() // Error
```

```swift

struct Person {
    var name: String
}

var person = Person(name: "John")

print(person.name) // John
```

```swift

class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person = Person() // Error
```

```swift

class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person = Person(name: "John")

print(person.name) // John
```


Class'lar inheritance yapabilir. Struct'lar yapamaz.

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

class Student: Person {
    var studentNumber: Int
    init(name: String, studentNumber: Int) {
        self.studentNumber = studentNumber
        super.init(name: name)
    }
}

var student = Student(name: "John", studentNumber: 123)

print(student.name) // John

print(student.studentNumber) // 123
```

```swift

struct Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

struct Student: Person { // Error
    var studentNumber: Int
    init(name: String, studentNumber: Int) {
        self.studentNumber = studentNumber
        super.init(name: name)
    }
}
```

Class'lar deinit metodu ile bellekten temizlenir. Struct'lar ise deinit metodu bulundurmaz.

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
    deinit {
        print("Person deinit")
    }
}

var person: Person? = Person(name: "John")

person = nil // Person deinit
```

```swift

struct Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person: Person? = Person(name: "John")

person = nil
```

Class'larda type casting yani tür dönüşümü yapılabilir. Struct'larda yapılamaz.





