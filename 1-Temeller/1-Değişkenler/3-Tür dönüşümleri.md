## Tür Dönüşümleri

Swift'te tür dönüştürebilmek için doğrudan tür adı ve parantezler kullanılır.

Örneğin Int bir değeri Double'a dönüştürmek için:

```
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
```

## typealias

Swift'te istersek kendimizde bir tür oluşturup buna isim verebiliriz. Buna typealias ismi veriliyor.

Örneğin:

```
typealias AudioSample = UInt16
var maxAmplitudeFound = AudioSample.min
```

