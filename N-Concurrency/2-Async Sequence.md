## Async Sequence

Swift 5.5 ile eklenen bu özellik asenkron operasyonların diziler halinde temsil edilmesini sağlar ve asenkron bir şekilde elemanları üretmeyi destekler.

Bir asenkron diziyi tanımlamak için `AsyncSequence` protokolünü kullanabiliriz:

```swift
func makeAsyncSequence() async -> AsyncSequence<Int> {
    return AsyncSequence { continuation in
        Task {
            for i in 1...5 {
                await Task.sleep(1_000_000_000) // 1 saniye bekle
                continuation.yield(i)
            }
        }
    }
}

Task {
    let asyncSeq = await makeAsyncSequence()

    for await number in asyncSeq {
        print(number)
    }
}
```