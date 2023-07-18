# ジェネリクス_2

## ジェネリクスを使った複数のプロパティ

- 以下はどんなデータ型も受け入れるが、first と second が同じデータ型である必要がある

```swift
struct Pair<T> {
    var first: T
    var second: T
}

// これはOK
let names = Pair(first: "Tomo", second: "Shimizu")

// これはNG
let names = Pair(first: "Tomo", second: 27)
```

- 特定のプロトコルに準拠させることもできる

```swift
struct Point<T: Numeric> {
    var x: T
    var y: T
}

let floats: Point<CGFloat> = Point(x: 1.5, y: 1.5)
let doubles: Point<Double> = Point(x: 1.5, y: 1.5)
```

---

## ジェネリックなカウントセット

- 一度型をジェネリックで宣言すれば、ジェネリック型のパラメータはその型に属する全てのメソッドで利用できるようになる

```swift
// NSCountedSetを模倣したカウントセット
struct CountedSet<T: Hashable>: Equatable, Hashable {
    private var elements = [T: Int]()
    var count: Int { elements.count }
    var isEmpty: Bool { elements.isEmpty }

    mutating func insert(_ element: T) {
        elements[element, default: 0] += 1
    }

    mutating func remove(_ element: T) {
        elements[element, default: 0] -= 1
    }

    func count(_ element: T) -> Int {
        elements[element, default: 0]
    }
}
```

- Hashable（ハッシュ可能）な任意のデータ型を格納できる

```swift
var set = CountedSet<String>()

// 要素の挿入
set.insert("Apple")
set.insert("Orange")
set.insert("Apple")

// 要素のカウント
set.count

// 要素の削除
set.remove("Apple")
```

---

## ジェネリックなパラメータの拡張