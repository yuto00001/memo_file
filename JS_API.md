目次
- [1. ●**Intersection Observer APIについて**](#1-intersection-observer-apiについて)
  - [1.1. ●**intersectionObserverについての説明**](#11-intersectionobserverについての説明)
  - [1.2. ●**Intersection Observerを使う**](#12-intersection-observerを使う)
- [2. ●**オプション (threshold) を指定する**](#2-オプション-threshold-を指定する)
  - [2.1. ●**要素が交差したらクラスを付け外しする**](#21-要素が交差したらクラスを付け外しする)
  - [2.2. ●**root , rootMarginオプションについて**](#22-root--rootmarginオプションについて)
    - [2.2.1. options](#221-options)
  - [2.3. ●**targetの監視を止める**](#23-targetの監視を止める)
  - [2.4. ●**すべての要素に処理を設定する**](#24-すべての要素に処理を設定する)
---

# 1. ●**Intersection Observer APIについて**
>こちらの API ですが、日本語では`交差監視 API` とよばれていて、`ある要素を監視して`、その要素がスクロールして特定の領域に入ってきたときに`どれだけその領域と交差したかを調べる`ことができるという仕組みです。

- `target`
  - 監視する領域
- `root`
  - targetが交差していく領域
- `Intersection Ratio`
  - targetがどのくらいrootと交差したかの割合

![google](/img/api.png)
>例えば、 target がこちらの画像で、このくらい交差していたとき、 target の 20% くらいが root に交差しているので、 Intersection Ratio は 20% くらいといった計算をしてくれます。

>また、`この Intersection Ratio の値に応じて処理を設定することができて`、例えば、この画像が viewport に `20% くらい交差したときに、ふわっと表示させる`といった処理も作ることができます。  
もしくは、ページの最後のほうに配置した要素が viewport に `100% 交差したときに次の要素を読み込んであげる`だとか、もしくはページの下のほうに配置していた広告が `viewport で 80% 表示されたらその広告が見られたと判断する`といった処理も作ることができます。
```JavaScript

```
```JavaScript

```

## 1.1. ●**intersectionObserverについての説明**
>以前のレッスンで Post クラスのインスタンスを作られたと思いますが、今回のレッスンで`IntersectionObserver のインスタンスを作るという場合`も同様に `IntersectionObserver クラスの`インスタンスを作っていると考えてよいです。

>Post クラスはメッセージの投稿に関するデータとその操作を集めたものだったかと思いますが、今回のIntersectionObserver クラスは`あらかじめブラウザが用意してくれているクラス`で、 オブジェクトと表示領域の **`重なりを監視するために必要なデータや処理をまとめたクラス`** であると認識して良い。

>`post = new Post(); `のような形で Post クラスのインスタンスを作ったかと思いますが、同様にIntersectionObserver のインスタンスは const observer = new IntersectionObserver(callback); で作っています。
そして、`この observer が` IntersectionObserver の`インスタンスとなり`、監視対象の`オブジェクトが画面に表示されたかどうかチェック`し、 **`条件に当てはまれば callback に指定した処理を実行`** します。
```JavaScript
'use strict';

{
  const target = document.querySelector('img');

  function callback() {
    console.log('fired!');
  }

  const observer = new IntersectionObserver(callback);

  observer.observe(target);
}
```
>IntersectionObserver クラスを `new することで新しいインスタンスを observer に代入`しています。↓  
（なお IntersectionObserver は JavaScript が最初から持っているクラスであって、自分で定義するものではありません）
```JavaScript
const observer = new IntersectionObserver(callback);
```
>今回は以下のようにしていますから、上記の callback 関数が呼び出されます。
つまりコンソールに fired! と出力されます。↓
```JavaScript
new IntersectionObserver(callback)
```
>この時点ではまだ`「何を監視するか」が指定されていません`ね。
それを指定しているのがこちらです。↓
```JavaScript
observer.observe(target);
```
>こうすることで observer に
「`target を監視対象としてください`」
と伝えることができます。  
この `target は`1行目で用意した target です。
つまり `img 要素`です。


```JavaScript

```
```JavaScript

```
## 1.2. ●**Intersection Observerを使う**
>次に Intersection Observer のインスタンスを作ってあげます。  
new IntersectionObserver(); としてあげれば OK です。  

```JavaScript
'use strict';
{
const target = document.querySelector('img');

function callback() {
  console.log('fired');
}
//3 こちらに書いていく処理ですが、とりあえず callback が呼ばれたよという意味で、コンソールに fired! と表示してみましょう。
// それから、こちらの処理が実行されるタイミングですが、監視が始まったときと、デフォルトだと target が root に 0% 交差したときに実行されます。

const observer = new IntersectionObserver(callback);
//2 あとは、この target が root に交差したときの処理を書きたいのですが、こちらに関数を渡してあげて、その中に書いていけば OK です。ではとりあえず、 callback という名前にしてあげて、上のほうで定義していきましょう。

observer.observe(target);
//1 そのあとに、この observer の observe() メソッドを使って target を監視してあげれば OK です。

}
```
>このようにこちらの処理ですが、`監視が始まったとき`と`スクロールしていって(デフォルトだと) target が 0% 交差したとき(頭と尻の計２回)`に実行される、という挙動をまずは理解しておいてください。
# 2. ●**オプション (threshold) を指定する**
デフォルトの0%ではなく、`指定した任意の % で、処理を実行する`。
>どうするかというと、こちらに`第二引数を渡`してあげて、そちらで設定してあげます。
```JavaScript
'use strict';

{
  const target = document.querySelector('img');

  function callback() {
    console.log('fired!');
  }

  const options = {
    threshold: [0.2, 0.8],
  };
  // 2 ではこの options ですが、 20% 交差したときとしたい場合はオブジェクト形式にしてあげて、 threshold というキーで 0 から 1 の値を指定すればいいので、 20% の場合はこのようにすれば OK ですね。
  // もしくは複数の値を指定したい場合は、配列にしてあげて、 20% と 80% の場合はこのように書いてあげれば OK です。

  const observer = new IntersectionObserver(callback, options);
  // 1 では、 第二引数をoptions としてあげましょう。

  observer.observe(target);
}
```
## 2.1. ●**要素が交差したらクラスを付け外しする**
>要素が交差したらクラスを付け外しすることで表示を制御していきます。  
要素が交差したらフワッと表示させましょう。

>スクロールしていくと、 20% くらい交差したところでふわっと画像が現れて、そのままスクロールしていくと、消えるときにはアニメーションしていないので OK そうです。

>`isIntersectingはターゲット要素が交差している場合に True になります`。レッスンで言うと img 要素がブラウザ画面の中に入ってきた or 外に出ていくタイミングで True になります。
```JavaScript
'use strict';

{
  const target = document.querySelector('img');

  function callback(entries) {
    console.log(entries[0]);

    if (!entries[0].isIntersecting) {
      return;
    }
    // 交差が始まったときに appear クラスを付ければいいので、 isIntersecting を調べてあげて、それが true だったら appear クラスを付けてあげればいいでしょう。ただ、交差が終わるときはアニメーションしてほしくない場合もありますね。
    // その場合ですが、下記の else の処理を削ってあげるか、もしくは isIntersecting が false のときは、早期 return してあげるという書き方もよく使われます。

    entries[0].target.classList.add('appear');
    // クラスを付ける要素ですが、 entries[0] の target で取得できるので、そちらに対して classList.add としてあげれば OK でしょう。

    // if (entries[0].isIntersecting) {
    //   entries[0].target.classList.add('appear');
    // } else {
    //   entries[0].target.classList.remove('appear');
    // }
  }

  const options = {
    threshold: 0.2,
  };

  const observer = new IntersectionObserver(callback, options);

  observer.observe(target);
}
```
## 2.2. ●**root , rootMarginオプションについて**
>thresholdの他に指定することができる、rootとrootMarginオプションについて見ていきます。

### 2.2.1. options
- `root`
  - `デフォルト値` null (ブラウザの viewport)
  - `特定の値` ex) document.querySelector('.クラス名'),
- `rootMargin`
  - `デフォルト`は 0px
>(root) ただ、`特定の要素を root にしたい場合`もあって、例えば、動画サイトなどによくありますが、横スクロールできる領域をページ内に複数設置して、`それぞれに observer を設定するような場合`ですね。  
その場合ですが、こちらに設定した observer の root には、こういった領域、こちらのほうに設置した observer の root にはこの領域といった具合に設定します。
![google](/img/options.png)

>(rootMargin) `root 領域の大きさを調整するためのオプション`で CSS の margin のように設定。  
これを変更したい場合ですが、たとえば、 CSS での指定のように、 0px 0px 100px とすると、下方向にだけ 100px の margin が付くので root 領域がこの領域になります。  
もしくは、 0px 0px -100px とすると、下方向に -100px の margin が付くので、こういった領域になりますね。
![google](/img/root_margin.png)

>一例ではありますが、たとえば root は viewport のままで `threshold を 1 に`して、`画像が 100% 交差したときにふわっと表示`させたとしましょう。  
ただここで、もう少し上のほうでふわっと表示させたかったとします。  
その場合ですが rootMargin を指定してあげて、 0px 0px -100px としてあげると、 root の領域がこの領域になります。  
そうすると、 root と target が 100% 交差するのは、このあたりの位置になるので、さきほどの場合と比べて少し上のほうでふわっと表示させることができるというわけですね。
![google](/img/root_ex.png)

```JavaScript
'use strict';

{
  const target = document.querySelector('img');

  function callback(entries) {
    console.log(entries[0]);

    if (!entries[0].isIntersecting) {
      return;
    }

    entries[0].target.classList.add('appear');
  }

  const options = {
    threshold: 1,
    rootMargin: '0px 0px -100px',
  };

  const observer = new IntersectionObserver(callback, options);

  observer.observe(target);
}
```
## 2.3. ●**targetの監視を止める**
>上記では、いったん監視を始めると、交差するたびに callback が実行されて、ブラウザに負荷がかかってしまいます。  
そこで、最初に画像がふわっと表示されたあとは監視を止めたいという場合を見ていきましょう。  
その場合なのですが、少しややこしいのですが、こちらの第二引数に、この関数を実行している observer を渡すことができます。
```JavaScript
// コードの一部を記載
  const target = document.querySelector('img');

// わかりやすいように定数名を変えて、 observer の obs としましょう。
  function callback(entries, obs) {
    console.log(entries[0]);

    if (!entries[0].isIntersecting) {
      return;
    }

// そのうえで、 entries[0].target の監視を止めたい場合は、 unobserve というメソッドを使ってあげれば OK です。
// 要素を渡せばいいので、 entries[0].target としてあげれば OK でしょう。
    entries[0].target.classList.add('appear');
    obs.unobserve(entries[0].target);
  }
```
>ブラウザに余計な負荷をかけないためにも、こうした処理を書けるようになっておくと良いでしょう。
## 2.4. ●**すべての要素に処理を設定する**
>`この entries は複数の要素をもつ配列`で、`監視開始時点ではすべての target` が、そして `target が交差したときは、交差した target だけ`が要素として入ってくるという点に注意しておきましょう。  
では、交差したすべての画像に appear クラスを付けたいので、コードを変更していきます。

```JavaScript
'use strict';

{
  const targets = document.querySelectorAll('img');

  function callback(entries, obs) {
    console.log(entries[0]);

// ここで、 forEach を使ってあげれば良いでしょう。
// entries のそれぞれの要素を entry としてあげて、次の処理をしなさいと書いていってあげます。
    entries.forEach(entry => {
      if (!entry.isIntersecting) {
        return;
      }
      entry.target.classList.add('appear');
      obs.unobserve(entry.target);
    });
  }

  const options = {
    threshold: 1,
    rootMargin: '0px 0px -100px',
  };

  const observer = new IntersectionObserver(callback, options);

  targets.forEach(target => {
    observer.observe(target);
  });
}
```

