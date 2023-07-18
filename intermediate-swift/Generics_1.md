# ジェネリクス_1

## ジェネリクスとは

- クラス・構造体・関数の引数として受け取るデータ型を抽象的に宣言できる機能
- 型引数名には、```<T>``` がよく使われる
- Array, Dictionaty, Setもジェネリクス

### ジェネリクスがない世界

- 各データ型を受け取るクラス・構造体・関数を宣言する必要がある

```swift
func count(numbers: [Int]) {}
func count(numbers: [Double]) {}
func count(numbers: [CGFloat]) {}

count(numbers: [1, 2, 3])
count(numbers: [1.0, 2.0, 3.0])
```

### ジェネリクスがある世界

- 一つのクラス・構造体・関数で対応できる

```swift
// Numericに適合できるデータ型のみ受け付ける
func count<Number: Numeric>(numbers: [Number]) {}

count(numbers: [1, 2, 3])
count(numbers: [1.0, 2.0, 3.0])
```

---

## 動的ディスパッチ と 静的ディスパッチ

- 動的ディスパッチとは、ポリモーフィックな操作（メソッドや関数）のどの実装を実行時に呼び出すかを選択するプロセスのこと
    - **ビルド時** にデータ型を決定する
- 静的ディスパッチとは、コンパイル時に完全に解決されるポリモーフィズムの一形態
    - **コンパイル時** にデータ型を決定する
- 静的ディスパッチの方がパフォーマンスが高い

### 用語解説
| 用語 | 意味 |
| - | - |
| コンパイル | ソースコード（人間語）をオブジェクトコード（コンピューター語）に変換すること |
| ビルド | コンパイルしたファイルを一つにまとめ実行すること |

---

## チャレンジ

### 課題1

- 文字列または部分文字列の文字数を出力する関数

```swift
func count<T: StringProtocol>(string: T) -> Int {
    return string.count
}
```

### 課題2

- 任意の数の配列を受け取り、全ての値の平均を返す関数

```swift
func average<T: FloatingPoint>(numbers: [T]) -> T {
    let total = numbers.reduce(0, +)
    return total / T(numbers.count)
}
```

---

## 参考

[Static vs Dynamic Dispatch in Swift: A decisive choice](https://medium.com/@bakshioye/static-vs-dynamic-dispatch-in-swift-a-decisive-choice-cece1e872d)