目次

---

## ●**配列を作る**
>ゲームのスコアを管理したかったとして、score1 、 score2 、 score3 といった具合に管理していっても良いのですが、同じ意味合いのデータなので、この 3 つをまとめて同じ名前で扱えるようになったほうが便利かと思います。

>順番を表すこれらの数値はインデックス、もしくは添字というのですが、`配列ではインデックスは 1 番からではなくて 0 番から始まる`ので注意しておいてください。
```JavaScript
'use strict';

{
  // const score1 = 80;
  // const score2 = 90;
  // const score3 = 40;

  const scores = [80, 90, 40];
  console.log(scores);
}
```

## ●**配列の要素にアクセスする**
>列の定数名に [] をつけて、前回見たインデックスを書いてあげれば OK。
```JavaScript
'use strict';

{
  const scores = [80, 90, 40];
  console.log(scores[1]); // ＝　90

  scores[2] = 44;
  console.log(scores); //　＝　[80,90,44]

  scores = 10; //　＝　再代入はできない。

  console.log(scores.length);　＝　3
}
```

## ●**配列とループ処理を組み合わせる**
`ループ処理を使えばたくさんの要素があってもすっきりと処理が書ける`

配列の要素数が変化したとしても対応できるよう、処理する側の` i < 3;` を `i < score.length; `へと書き換える。`配列の要素数と表示させたい数が同じ`という点に着目したテクニック。
```JavaScript
'use strict';

{
  const scores = [80, 90, 40, 70];

  // console.log(`Score: ${scores[0]}`);
  // console.log(`Score: ${scores[1]}`);
  // console.log(`Score: ${scores[2]}`);

  // for (let i = 0; i < 3; i++) {

  // 今回はインデックスが 0 、 1 、 2 の要素について処理したいので、i が 0 から 3 未満の間 1 ずつ増やしながら次の処理をしなさい、と書いてあげれば良い。
  for (let i = 0; i < scores.length; i++) {
    console.log(`Score ${i}: ${scores[i]}`);
  }
}
```

## ●**配列の要素を変更する**
配列には、先頭や末尾の要素を操作するための便利な命令が用意されている。

![google](/img/hairetu.png)
```JavaScript
'use strict';

{
  const scores = [80, 90, 40, 70];
  scores.push(60, 50);
  scores.shift();
  // 90, 40, 70, 60, 50

  for (let i = 0; i < scores.length; i++) {
    console.log(`Score ${i}: ${scores[i]}`);
  }
}
```

## ●**splice()で配列を変更する**
>前回見た命令は配列の先頭や末尾を操作するためのものでしたが、`途中の要素も操作できるのが splice() という命令。`

```JavaScript
splice(変化が開始する位置, 削除数)
splice(変化が開始する位置, 削除数, 追加する要素, ... )
```
```JavaScript
'use strict';

{
  const scores = [80, 90, 40, 70];
  scores.splice(1, 1, 40, 50);
  // splice(変化が開始する位置, 削除数, 追加する要素, ... )
  // 80, 40, 50, 40, 70

  for (let i = 0; i < scores.length; i++) {
    console.log(`Score ${i}: ${scores[i]}`);
  }
}
```

## ●**スプレッド構文を使う**
スプレッド構文　＝　 ひとつのデータ配列に対してもう一つのデータ配列を挿入したい場合に、`記号[ ... ]を用いて記述された構文`のこと。
```JavaScript
'use strict';

{
  const otherScores = [10, 20];
  const scores = [80, 90, 40, 70, ...otherScores];
  // console.log(scores);

  function sum(a, b) {
    console.log(a + b);
  }

  sum(...otherScores);
  // sum(10, 20);
}
```

## ●**分割代入を使う**
分割代入　＝　 ひとつのデータ`配列の定数を、別の定数に変更する`こと。
```JavaScript
'use strict';

{
  const scores = [80, 90, 40, 70];

  // const [a, b, c, d] = scores;
  // console.log(a);
  // console.log(b);
  // console.log(c);
  // console.log(d);
  // = 80, 90, 40, 70

  // const [a, b, ...others] = scores;
  // console.log(a);
  // console.log(b);
  // console.log(others);
  // = 80, 90, [40, 70]

// 分割代入による値の交換。
  let x = 30;
  let y = 70;
  [x, y] = [y, x];
  console.log(x);
  console.log(y);
}
```

## ●**forEach()を使う**
for() = 文字列に変数の値を埋め込む記法。
>forEach() は少しくせがありますが、 for 文を使った処理と違って、`要素数などを気にせずにすっきりと処理が書ける`ので、使いこなせるようになっておくと良いでしょう。
```JavaScript
'use strict';

{
  const scores = [80, 90, 40, 70];

  // scores.forEach((score) => {
  scores.forEach((score, index) => {
    console.log(`Score ${index}: ${score}`);
    // Score 0: 80, Score 1: 90...
  });
}
```
## ●**map()を使う**
`配列に何らかの処理をして、その結果を別の配列として取得したいという場合`
>このように配列の各要素に何らかの処理をして別の配列を作りたい場合は map() が便利なので覚えておくと良いでしょう。
```JavaScript
'use strict';

{
  const prices = [180, 190, 200];

  // const updatedPrices = prices.map((price) => {
  //   return price + 20;
  // });

// まず引数が 1 つの場合はこちらの () は省略して OK です。
// それから return の 1 行の場合は、このあたりも省略して OK でしたね。
  const updatedPrices = prices.map(price => price + 20);
  console.log(updatedPrices);
  // [200, 210, 220]
}
```
## ●**filter()を使う**
filter() = `配列の要素をチェックして、条件にあうものだけを抽出して別の配列として取得する`ことができる。
>例として、下記に偶数の要素だけを別の配列として抽出する。
```JavaScript
'use strict';

{
  const numbers = [1, 4, 7, 8, 10];

  // const evenNumbers = numbers.filter(number => {
  //   if (number % 2 === 0) {
  //     return true;
  //   } else {
  //     return false;
  //   }
  // });
  const evenNumbers = numbers.filter(number => number % 2 === 0);

  console.log(evenNumbers);
  // [4, 8, 10]
}
```
## ●**オブジェクトを作る**
>今まで見てきた配列は複数の値に順番を付けてまとめたものでしたが、`値に名前を付けて管理することができるオブジェクト`についても見ていきましょう。

>では、今お絵かきアプリなどを作っていて、点の座標を管理したかったとします
```JavaScript
'use strict';

{
  // const point = [100, 180];

  // const point = {x: 100, y: 180};
  const point = {
    x: 100,
    y: 180,
  };
  console.log(point);
  // {x: 100, y:180} 値が名前付きで管理されている
}
```
- プロパティ（メンバー）
- 名前（キー）
- 値
![google](/img/object.png)

## ●**プロパティを操作する**
`オブジェクトのプロパティにアクセスする方法`

```JavaScript
'use strict';

{
  const point = {
    x: 100,
    y: 180,
  };

  point.x = 120;
  // point['x'] = 120;

  // プロパティにアクセスする方法↓
  // console.log(point.x);
  // console.log(point['y']);

// それから、プロパティを追加したり削除したりする方法も見ておきます。
// こちらのオブジェクトに Z 座標を追加したかった場合、新しいキーで値を設定してあげればプロパティが作られる
  point.z = 90;
  delete point.y;
  console.log(point);
  // {x: 120, z: 90}
}
```
## ●**オブジェクトを操作する**
>前に スプレッド構文で配列を展開する方法を紹介しましたが、`スプレッド構文はオブジェクトを展開するためにも使うことができる`。
[解説動画URL](https://dotinstall.com/lessons/basic_javascript_objects_v2/52313)

```JavaScript
'use strict';

{
  const otherProps = {
    r: 4,
    color: 'red',
  };

  const point = {
    x: 100, 
    y: 180,
    ...otherProps,
  };
  // console.log(point);

  const {x, r, ...others} = point;
  console.log(x);
  console.log(r);
  console.log(others);
  // 100
  // 4
  // {y: 180, color: "red"}
}
```
## ●**Object.keys()を使う**
Object.keys()を使って、オブジェクトのプロパティ一つひとつに対して処理をする方法と、配列の中にオブジェクトを入れる方法
>ブジェクトのプロパティを列挙したいが、`オブジェクトには forEach() が使えない`ので、いくつかの手順を踏む必要がある。

>少し奇妙な命令だが、 `Object.keys(point)` とすると `point の全てのキーを配列で取得`できるので、それを keys という定数にまずは入れる。そうすると`キーが配列で取得`できて、`配列には forEach() が使える`ので、それを使う。
```JavaScript
'use strict';

{
  const point = {
    x: 100,
    y: 180,
  };

  // const keys = Object.keys(point);
  // keys.forEach(key => {
  //   console.log(`Key: ${key} Value: ${point[key]}`);
  // });

  const points = [
    {x: 30, y: 20},
    {x: 10, y: 50},
    {x: 40, y: 40},
  ];
  console.log(points[1].y);
  // 50
}
```
## ●**変数を代入する**
単純なデータ型と配列やオブジェクトで、変数を代入したときの挙動が異なる。

単純なデータ型(数値や文字列)：  
複雑なデータ型(配列やオブジェクト)：
```JavaScript
'use strict';

{
  let x = 1;
  let y = x;
  x = 5;
  console.log(x); // 5
  console.log(y); // 1

  let x = [1, 2];
  let y = x;
  x[0] = 5;
  console.log(x); // [5, 2]
  console.log(y); // [1, 2]になりそうだが、結果は[5, 2]となる。
}
```
![google](/img/hensu.png)
>なぜこのような仕組みになっているかについては、複雑なデータ型はデータ量が大きくなることも多いので、`丸ごと値をコピーしてシステムに負荷をかけてしまわないため`、と理解しておいても良い

それでも配列やオブジェクトの値を丸ごとコピーして使いたいという場合には、スプレッド演算子がよく用いられる。
>以下のように記述すると、x の値が展開され、 y には x の値がある場所ではなく、こちらの [1, 2] という値そのものが代入される。
```JavaScript
'use strict';

{
  // let x = 1;
  // let y = x;
  // x = 5;
  // console.log(x); // 5
  // console.log(y); // 1

  // let x = [1, 2];
  // let y = x;
  // x[0] = 5;
  // console.log(x); // [5, 2]
  // console.log(y); // [5, 2]

  let x = [1, 2];
  let y = [...x];
  x[0] = 5;
  console.log(x); // [5, 2]
  console.log(y); // [1, 2]
}
```
## ●**文字列を操作する**
>ここまで配列とオブジェクトについて見てきましたが、 JavaScript には他にもデータを操作するための便利な命令がいろいろあるので、よく使うものを見ていきましょう。

```JavaScript
'use strict';

{
  const str = 'hello';

  // 文字列を扱うための命令
  console.log(str.length); // 5

  // str.substring(開始位置, 終了位置);
  console.log(str.substring(2, 4)); // ll

  // 文字列に対して配列のような記法を使うと、個々の文字にアクセスできる
  console.log(str[1]); // e
  // str[1] = 'a'; このように str[1] に対して値を設定したり、もしくは str に対して forEach() を使ったりできるわけではない
}
```
## ●**join(),split()を使う**
`join()` = 引数に結合するときの文字列を渡す。  
`split()` = 文字列を区切り文字で分割し、それを配列にする。
```JavaScript
'use strict';

{
  const d = [2019, 11, 14];

  console.log(d.join('/')); // 2019/11/14
  console.log(d.join('')); // 20191114

  const t = '17:08:24';
  console.log(t.split(':')); // ["17", "08", "24"]
  const [hour, minute, second] = t.split(':');
  console.log(hour); // 17
  console.log(minute); //08
  console.log(second); //24
}
```
## ●**数値を操作する**
>まずはこの数値の合計と平均を求めたかったとします。
```JavaScript
'use strict';

{
  const scores = [10, 3, 9];

  let sum = 0;

  scores.forEach(score => {
    sum += score;
  });

  const avg = sum / scores.length;

  console.log(sum); //22
  console.log(avg); //7.33333...

  console.log(Math.floor(avg)); // 7 小数点以下切り捨て
  console.log(Math.ceil(avg)); // 8 切り上げ
  console.log(Math.round(avg)); // 7 四捨五入
  console.log(avg.toFixed(3)); // 7.333 文字数指定

// 乱数を生成するための命令
// これは 0 以上 1 未満のランダムな数値を生成してくれます。
  console.log(Math.random());
}
```
## ●**ランダムな整数値を作る**

```JavaScript
'use strict';

{
  console.log(Math.random()); // 0 以上 1 未満のランダムな数値
  Math.floor(Math.random() * 3) // 0, 1, 2
  Math.floor(Math.random() * (n + 1)) // 0, ..., n
  Math.floor(Math.random() * (max + 1 - min)) + min // min, ..., max

  console.log(Math.floor(Math.random() * 6) + 1); // １~６の整数値
}
```
## ●**現在日時を扱う**
>定数を用意して、現在日時を表す値は new Date() で作ることができるので、これをそのまま表示してみましょう。

![google](/img/date_nitiji.png)
![google](/img/date_2.png)
```JavaScript
'use strict';

{
  const d = new Date();
  // console.log(d);

  console.log(`${d.getMonth() + 1} 月 ${d.getDate()} 日`);
  // ○月○日
}
```
>どのタイムゾーンで取得しても同じになるような値が用意されていて、 getTime() を使ってあげれば OK
## ●**特定の日時を扱う**
>前回見たようにこちらを使うと現在日時の値を取得できるのですが、特定の日時を表す値を作りたいときもあります。  
特定の日時を表す = `引数に年月日などを渡す`。

```JavaScript
'use strict';

{
  const d = new Date(2019, 10); // 2019/11/01 00:00:00
  d.setHours(10, 20, 30); // 2019/11/01 10:20:30
  d.setDate(31); // 2019/12/01 10:20:30
  d.setDate(d.getDate() + 3); // 2019/12/04 10:20:30
  console.log(d);
}
```
## ●**alert(),confirm()を使う**
`警告や確認のダイアログを表示する方法`
```JavaScript
'use strict';

{
  alert('hello');

  // 何らかの処理の前に確認したい場合
  const answer = confirm('削除しますか？'); // アラート内容に加えて、okボタンと cancelボタンが表示される。

  // ここで、どちらが押されたかは confirm() の返り値で取得することができるので、こちらはいったんキャンセルして confirm() の返り値を answer という定数で受け取ってみましょう。
  if (answer) {
    console.log('削除しました');
  } else {
    console.log('キャンセルしました');
  }
}
```
## ●**setInterbval()を使う**
`タイマー機能`
```JavaScript
'use strict';

{
  let i = 0;

  function showTime() {
    console.log(new Date());
    i++;
    if (i > 2) {
      clearInterval(intervalId);
    }
  }

  const intervalId = setInterval(showTime, 1000);
}
```
## ●**setTimeout()を使う**
setTimeout() = `指定した時間のあとに 1 回だけ処理を実行するように予約する命令`。
```JavaScript
'use strict';

{
  let i = 0;

  function showTime() {
    console.log(new Date());
    const timeoutId = setTimeout(showTime, 1000);
    i++;
    if (i > 2) {
      clearTimeout(timeoutId);
    }
  }

  showTime();
}
```
## ●**タイマー処理の違いを理解する**
 setInterval() = `一定時間ごとに処理を実行するための命令`。  
 setTimeout() = `一定時間後の処理が完了するたびに実行するための命令`。
![google](/img/setInterval.png)
>もし処理に 1200 ミリ秒かかる場合でも setInterval() では 1000 ミリ秒きっかりに処理を実行しようとするので、このように 2 つの処理が重なってシステムに負荷がかかってしまう場合もあります。

![google](/img/setTimeout.png)
>システムに負荷をかけずにくり返し処理を実行したい場合は setTimeout() もよく使われる
---
## ●**例外処理を使う**
>ユーザーから名前を受け取って、それを大文字にするという処理を考えてみます。

>他にもネットワークが繋がらなくなったり、ハードウェアが故障した場合などに例外が発生し得るのですが、それでも処理を止めたくない場合があります。

>そのようなときに使えるのが例外処理で、どのようなものかというと、`例外が起きそうな箇所をまずは try {} で囲って`あげます。そのうえで `catch で続けて例外が起きたときの処理`をこちらに書いていけば OK

`大文字にするには toUpperCase() `という命令を使う。
```JavaScript
'use strict';

{
  // const name = 'taguchi';
  const name = 5;

  try {
    console.log(name.toUpperCase());
  } catch (e) {
    console.log(e);
  }

  console.log('Finish!');
}
```
---
---
---
# ●**オブジェクトが複数ある場合を考える**

## ●**メソッドを使う**
>実はオブジェクトではプロパティの値として、関数を持たせることもできます。
```JavaScript

```
## ●**　**

```JavaScript

```
## ●**　**

```JavaScript

```
## ●**　**

```JavaScript

```
## ●**　**

```JavaScript

```
## ●**　**

```JavaScript

```
