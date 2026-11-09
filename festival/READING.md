# 読解ノート：自分のアプリのコード3箇所

> **氏名：** カウン　ミャット　トゥー
> **AI利用レベル：** 1（質問のみ。説明は自分の言葉で書く）
> **最終更新：** 2026-11-09

生成AIに書いてもらったコードでも、自分で書いたコードでもかまいません。自分のアプリの中から3箇所を選んで、次の3つの問いに答えてください。分からないところは、生成AIに「この行は何をしていますか」「この行を消すとどうなりますか」と聞いてかまいません。ただし、書くのは自分の言葉です。

> 💡 担任の先生の指示で、項目が増えることがあります。

---

## 箇所1：ブックマークの保存

```swift
func toggle(_ key: String) {
    if !favorites.insert(key).inserted { favorites.remove(key) }
    UserDefaults.standard.set(favorites.sorted(), forKey: "favorites")
}）
```

**何をしているか：**
お気に入りの切り替えをして、保存する処理です。

**なぜこう書くのか：**
無駄を省いて一回で終わらせるため です。

**もしこう書かなかったら：**
2行目をコメントアウトして再起動すると、アプリを使っている間は問題なく動きます。画面上でお気に入りの追加・削除ができます。
でもアプリを再起動したあとは変更がすべて消えて再起動前の保存状態に戻ってしまいます。
---


## 箇所2：誕生日から星座を決める

```swift
let month = value / 100, day = value % 100
let days = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
guard (1...12).contains(month), (1...days[month - 1]).contains(day) else { return nil }
switch value {
case 120...218: return "Aqr"
case 219...320: return "Psc"
case 321...419: return "Ari"
case 420...520: return "Tau"
case 521...620: return "Gem"
case 621...722: return "Cnc"
case 723...822: return "Leo"
case 823...922: return "Vir"
case 923...1022: return "Lib"
case 1023...1121: return "Sco"
case 1122...1221: return "Sgr"
default: return "Cap"
}
```

**何をしているか：**
数字（例: 214 ＝ 2月14日）から「星座」を割り出す処理です。

**なぜこう書くのか：**
短くて計算が速く、変な日付をしっかり弾けるからです。

**もしこう書かなかったら：**
default を別の星座の case に書き換えると、1月1日は『やぎ座』ですが、年をまたぐせいで数字が浮いてしまい、みごとな迷子になります.
---


## 箇所3：タップした星を探す

```swift
var best: SkyStar?
var bestDist: CGFloat = 44
for s in SkyStar.all {
    let p = project(CGPoint(x: s.x, y: s.y), 1, t, size)
    let d = hypot(p.x - pt.x, p.y - pt.y)
    if d < bestDist { bestDist = d; best = s }
}
```

**何をしているか：**
タッチした場所に一番近い星を探し出す処理です。

**なぜこう書くのか：**
宇宙の星を画面の座標に置き換え、指から44pt以内にある『一番近い星』だけを正確に選ぶため

**もしこう書かなかったら：**
もし　CGFloat の　44を5や200に変えてみられば５にすると難しすぎて押せば、200にすると適当に押しても安全対応してしまいます。

---


## 自分ではまだ説明できない箇所（正直に）

（アプリの中で「動いているけれど何をしているか分からない」ところを書く。ここに書いたものは、後期の文法の授業で分かるようになります。）
