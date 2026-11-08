# 読解ノート：自分のアプリのコード3箇所

> **氏名：** 梶田陽斗
> **AI利用レベル：** 1（質問のみ。説明は自分の言葉で書く）
> **最終更新：** 2026-10-23

生成AIに書いてもらったコードでも、自分で書いたコードでもかまいません。自分のアプリの中から3箇所を選んで、次の3つの問いに答えてください。分からないところは、生成AIに「この行は何をしていますか」「この行を消すとどうなりますか」と聞いてかまいません。ただし、書くのは自分の言葉です。

> 💡 担任の先生の指示で、項目が増えることがあります。

---

## 箇所1：タブによる画面切り替え処理

```
switch erabu {
case 0:
    ContentView()
case 1:
    BattleEntryView(
        taibuKesu: $taibuKesu,
        oto: oto
    )
default:
    SavedListView()
}
```
**何をしているか：**
（この部分が果たしている役割を説明する）
画面下のボタンで選択した内容によって、合成画面、対戦画面、保存一覧画面を切り替える処理をしている。

**なぜこう書くのか：**
（別の書き方ではなく、この書き方が選ばれている理由を説明する。分からなければ「分からない」と書いてよい）
3つの画面を切り替える必要があるため、switch文を使うことで、どの画面を表示するのか分かりやすくできるから。

**もしこう書かなかったら：**
（この部分を消したり変えたりすると何が起きるか。実際に試した結果があればここに書く）
この処理を消してしまうと、選択したボタンに応じて画面を切り替えることができなくなる。

---

## 箇所2：タイトル画面からメイン画面への移動

```
.navigationDestination(isPresented: $idou) {
    GameFadeIn {
        MainTabView()
            .navigationBarBackButtonHidden(true)
    }
}


```
**何をしているか：**
ゲームをはじめるボタンを押した後に、タイトル画面からメイン画面に移動する処理をしている。また、移動した後に左上の戻るボタンが表示されないようにしている。

**なぜこう書くのか：**
画面を移動するタイミングを管理し、演出が終わった後にメイン画面を表示できるようにするため。また、戻るボタンを非表示にすることで、間違えてタイトル画面に戻らないようにしている。

**もしこう書かなかったら：**
画面を移動する処理がなくなるため、ゲームをはじめるボタンを押してもメイン画面に移動できなくなる。また、戻るボタンを非表示にする部分を消すと、左上に戻るボタンが表示されるようになる。

---

## 箇所3：GIF背景の表示設定

```swift
let webView = WKWebView()

webView.isOpaque = false
webView.backgroundColor = .clear
webView.scrollView.backgroundColor = .clear

webView.scrollView.isScrollEnabled = false
webView.scrollView.bounces = false
```

**何をしているか：**
GIFアニメーションを表示するためのWebViewを作成しています。また、背景を透明に設定したり、画面がスクロールしないようにしたりしている。

**なぜこう書くのか：**
GIFアニメーションを表示する際に、余計な背景が表示されたり、画面が動いてしまったりするのを防ぐため。

**もしこう書かなかったら：**
背景を透明にする設定を消すと、WebViewの背景色が表示される場合がある。また、スクロールを禁止する処理を消すと、GIFを表示している部分がスクロールしたり、引っ張ったときに動いたりする可能性がある。

---

## 自分ではまだ説明できない箇所（正直に）
```
struct GIFView: UIViewRepresentable {

    func makeUIView(context: Context) -> WKWebView {
        let webView = WKWebView()
        return webView
    }

    func updateUIView(
        _ uiView: WKWebView,
        context: Context
    ) {
    }
}
```
IViewRepresentable を使うと、なぜUIKitの部品をSwiftUIで表示できるのかと、なぜ普通の View ではなく UIViewRepresentable を使うのかがよく理解できないです。
（アプリの中で「動いているけれど何をしているか分からない」ところを書く。ここに書いたものは、後期の文法の授業で分かるようになります。）
