# オプショナルを取り除く方法

## 1. compactMap()を使う

* compactMap()は、配列内のnilを除去した配列を返す関数
* 配列のデータを使用して、nilになる可能性のある別のデータ型の配列に変換するときによく使われる

```swift
let numberStrings = ["1", "2", "Three"]
let numberInts = numberStrings.compactMap { Int($0) }
```

```swift
let urlStrings = ["https://apple.com", "https://swift.org", ""]
let urls = urlStrings.compactMap { URL(string: $0) }
```

---

## 2. 遅延格納プロパティ(Lazy stored property)を使う

* 遅延プロパティは、変数が使用されるまで初期化処理を遅延させることができるプロパティ
* 初期値が他のプロパティに依存している場合は、設定が複雑で使用されるまで生成する必要がない場合に使う

```swift
// プロパティのみ
lazy var collectionView: UICollectionView {
    let collectionView = UICollectionView(frame: .zero)
    return collectionView
}

// プロパティとメソッドで分ける
lazy var collectionView = makeCollectionView()

func makeCollectionView() -> UICollectionView {
    let collectionView = UICollectionView(frame: .zero)
    return collectionView
}
```

---

## 3. throwsを使う

* Optionalの値を返す代わりにthrowsを使うことで、次のようなメリットがある
    * 単にnilを返すのではなく、なぜ失敗したのかがわかる
    * 関数を拡張して、さまざまな種類の失敗を返すことができるようになる

### Optionalの値を返す場合

```swift
func encrypt(key: String) -> String? {
    if key == "12345" {
        print("I have the same key on my luggage.")
        return nil
    }

    return "Encryption complete"
}
```

### throwsを使う場合

```swift
enum PasswordError: Error {
    case obvious
}

func encrypt(key: String) throws -> String {
   if key == "12345" {
      print("I have the same key on my luggage.")
      throw PasswordError.obvious
   }

   return "Encryption complete"
}
```