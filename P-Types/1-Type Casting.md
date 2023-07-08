## Type Casting

Çalışma zamanında bir değerin türünü kontrol etmek ve bu değeri başka bir türe dönüştürmek için kullanılır. Type casting, Swift dilinde, bir değerin türünü kontrol etmek için kullanılan is ve as operatörleri ile yapılır.

## Type Check Operator (is)

Bir değerin türünü kontrol etmek için kullanılır. Bir değerin türü, bir türün alt türü veya bir protokolün uygulaması olup olmadığını kontrol etmek için kullanılabilir. Boolean değer döndürür.

```swift
if someValue is String {
    print("someValue is String")
} else if someValue is Int {
    print("someValue is Int")
} else {
    print("someValue is not String or Int")
}
```

## Downcasting (as)

Bir değeri, bir türün alt türüne veya bir protokolün uygulamasına dönüştürmek için kullanılır. Dönüştürme işlemi başarılı olursa, dönüştürülen değer, dönüştürülen türün alt türü veya uyguladığı protokolün türüne dönüştürülür. Dönüştürme işlemi başarısız olursa, çalışma zamanı hatası oluşur.

```swift
let someValue: Any = "Hello, World!"
let stringValue = someValue as! String
print(stringValue)
```

Burada as? veya as! kullanabiliriz. as? kullanırsak, dönüştürme işlemi başarısız olursa nil döner. as! kullanırsak, dönüştürme işlemi başarısız olursa çalışma zamanı hatası oluşur.

```swift
class MediaItem {
    var name: String
    init(name: String) {
        self.name = name
    }
}

class Movie: MediaItem {
    var director: String
    init(name: String, director: String) {
        self.director = director
        super.init(name: name)
    }
}


class Song: MediaItem {
    var artist: String
    init(name: String, artist: String) {
        self.artist = artist
        super.init(name: name)
    }
}

for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.name), dir. \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}
```


