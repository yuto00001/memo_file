- [1. ●**改行やタブを文字列として表現する**](#1-改行やタブを文字列として表現する)
- [2. ●**複数の文字列をまとめて表示する**](#2-複数の文字列をまとめて表示する)
- [3. ●**さまざまな計算方法**](#3-さまざまな計算方法)
- [4. ●**定数の設定と指定**](#4-定数の設定と指定)
- [5. ●**変数の使い方**](#5-変数の使い方)
- [6. ●**変数計算の基礎**](#6-変数計算の基礎)
- [7. ●**JS のデータ型について**](#7-js-のデータ型について)
- [8. ●**比較演算子について**](#8-比較演算子について)
- [9. ●**条件分岐について**](#9-条件分岐について)
- [10. ●**条件演算子について**](#10-条件演算子について)
- [11. ●**論理演算子について**](#11-論理演算子について)
- [12. ●**switch で条件分岐をする**](#12-switch-で条件分岐をする)
- [13. ●**for を使ってループ処理をする**](#13-for-を使ってループ処理をする)
- [14. ●**while を使ったループ処理**](#14-while-を使ったループ処理)
- [15. ●**関数で処理をまとめる**](#15-関数で処理をまとめる)
- [16. ●**引数を使う**](#16-引数を使う)
- [17. ●**return で値を返す**](#17-return-で値を返す)
- [18. ●**関数式を使う**](#18-関数式を使う)
- [19. ●**アロー関数**](#19-アロー関数)
- [20. ●**スコープについて理解する**](#20-スコープについて理解する)
- [21. ●**コードをブロックで囲う**](#21-コードをブロックで囲う)

---
---


※'use strict' ;　＝　厳密なエラーチェックをするためのもの。書いておくとエラーが発見しやすくなる。
JS の`最上部に絶対書く`

---

## 1. ●**改行やタブを文字列として表現する**
\　 ＝　直後の記号等を文字列として扱う  
\n 　＝　改行  
\t 　＝　タブ

```JavaScript
console.log('hel\nlo wor\tld');
```

## 2. ●**複数の文字列をまとめて表示する**

```JavaScript
console.log('hello' + 'world');
```

## 3. ●**さまざまな計算方法**

```JavaScript
console.log(10 + 3); // 13
console.log(10 - 3); // 7
console.log(10 * 3); // 30
console.log(10 / 3); // 3.333...
console.log(10 % 3); // 1
console.log(10 ** 3); // 1000

console.log(2 + 10 * 3); // 32
console.log((2 + 10) * 3); // 36
```

---

## 4. ●**定数の設定と指定**

プログラムの可変性を考えると、定数は積極的に用いるべきである。

```JavaScript
const price = 150;

console.log(price * 140);
console.log(price * 160);
```

## 5. ●**変数の使い方**

変数は、一度設定した値を再度設定し直すことができる。

> 定数と変数の使い分けは、ある名前に割り当てた値がころころ変わるとわかりづらいので、なるべく const を使いつつ、どうしても必要なときに let を使うという方法がよく取られます。  
> また、変数を宣言するのに var というキーワードもあるが、古い書き方のため、let を用いるのが良い。

```JavaScript
// 定数 const
// 変数 let var

let price = 150;
console.log(price * 140);

price = 170;
console.log(price * 140);
```

## 6. ●**変数計算の基礎**

```JavaScript
let price = 500;

// price = price + 100;
price += 100; // 600

// price = price * 2;
price *= 2; // 1200

// price = price + 1;
// price += 1;
price++; // 1201

// price -= 1;
price--; // 1200

console.log(price);
```

---

## 7. ●**JS のデータ型について**

![google](/img/data.png)

> ※JavaScript では、数字からなる文字列も数値に変換して、演算できるということにまず注意しておきましょう。

## 8. ●**比較演算子について**

```JavaScript
const price = 1200;

console.log(price > 1000); // true
console.log(price < 1000); // false
console.log(price >= 1000); // true
console.log(price <= 1000); // false
console.log(price === 1000); // false
console.log(price !== 1000); // true

// false <- 0, null, undefined, '', false
// true <- それ以外
```

---

## 9. ●**条件分岐について**

> `if()`：  
> `switch()` :〇〇だったら △△、という命令が続く処理。  
> `for()` : 特定の処理をくり返し実行するためのループ処理。  
> `*while()` :指定した条件が満たされている間、特定の処理を繰り返す。

if 文の記述例

```JavaScript
const score = 40;

if (score >= 80) {
  console.log('Great!');
} else if (score >= 60) {
  console.log('Good.');
} else {
  console.log('OK...');
}
```

## 10. ●**条件演算子について**

記述方法

> `条件式 ? trueの処理 : falseの処理`

この構文は短かく書けるという利点の一方で、`場合によってはコードが読みにくくなる`欠点もある。

```JavaScript
const score = 85;

// if (score >= 80) {
//   console.log('Great!');
// } else {
//   console.log('OK...!');
// }
score >= 80 ? console.log('Great!') : console.log('OK...!');
```

## 11. ●**論理演算子について**

`二重の条件分岐などの複雑で読みづらい処理になる場合`、論理演算子を用いることによって短く、読みやすく表現することができる。

論理演算子で用いる記号

> `&& なおかつ（AND）`  
> `|| もしくは（OR）`  
> `! 〜ではない（NOT）`

```JavaScript
const score = 60;
const name = 'taguchi';

// if (score >= 50) {
//   if (name === 'taguchi') {
//     console.log('Good job!');
//   }
// }

if (score >= 50 && name === 'taguchi') {
  console.log('Good job!');
}
```

## 12. ●**switch で条件分岐をする**

`〇〇だったら△△。という命令が続く処理`には、switch()の条件分岐を使う。

- () の中に比較したい値をまずは入れる
- そのうえで、どの値と比較したいかを case のあとに書く。

```JavaScript
const signal = 'pink';

// if (signal === 'red') {
//   console.log('Stop!');
// } else if (signal === 'yellow') {
//   console.log('Caution!');
// } else if (signal === 'blue'){
//   console.log('Go!');
// }

switch (signal) {
  case 'red':
    console.log('Stop!');
    break;
  case 'yellow':
    console.log('Caution!');
    break;
  case 'blue':
  case 'green':
    console.log('Go!');
    break;
  default:
    console.log('Wrong signal!');
    break;
}
```

## 13. ●**for を使ってループ処理をする**

`文字列に変数の値を埋め込む記法。`

_※ i は 1 ずつ増やしながら値を再代入していくので、こちらでは` let が使われている`点にも注意。_  
カウンターの値もこちらの処理の中で表示するには、文字列に変数の値を埋め込む記法を用いる。

> 下記のコードの場合、i が 1 から 10 以下である間、 i を 1 ずつ増やしながら次の処理をする。

```JavaScript
for (let i = 1; i <= 10; i++) {
  // console.log('hello');
  // console.log('hello' + i);
  console.log(`hello ${i}`);
}
```

> テンプレートリテラルを使うには ' （シングルクォーテーション）の代わりに ` （バッククオート）という記号を使う。

## 14. ●**while を使ったループ処理**

指定した条件が満たされている間、特定の処理を繰り返す。

> 下記コードの場合、i が 4 になったら break されて、それ以降の処理は実行しない。

```JavaScript
for (let i = 1; i <= 10; i++) {
  // if (i === 4) {
  // if (i % 3 === 0) {
  //   continue;
  // }
  if (i === 4) {
    break;
  }
  console.log(i);
}
```
---
---
## 15. ●**関数で処理をまとめる**

> 関数で処理をまとめておくと、コードを書く量が減らせる上、あとで処理の内容を変更したくなったときでも、ここだけ修正すれば良くて便利。積極的に活用すべき。

```JavaScript
function showAd() {
  console.log('----------');
  console.log('--- Ad ---');
  console.log('----------');
}

showAd();
console.log('Tom is great!');
console.log('Bob is great!');
showAd();
console.log('Steve is great!');
console.log('Richard is great!');
showAd();
```

## 16. ●**引数を使う**

`場所によって表示する文言だけ変えたい場合など。`

> テンプレートリテラルを使ってメッセージを埋め込む。
>
> > 仮引数　＝　仮置きしている値  
> > 実引数　＝　実際に関数を呼び出すときに渡される処理

```JavaScript
function showAd(message = 'Ad') { // 仮引数
  console.log('----------');
  console.log(`--- ${message} ---`);
  console.log('----------');
}

showAd('Header Ad'); // 実引数
console.log('Tom is great!');
console.log('Bob is great!');
// デフォルト値として’Ad'が渡されているので、引数には何も入れなくて良い。ここに何か文字を加えることで、文言を変えることができる。↓
showAd();
console.log('Steve is great!');
console.log('Richard is great!');
showAd('Footer Ad');
```

## 17. ●**return で値を返す**

> return とはなんなのか　＝　`関数をそのまま式に入れて計算ができるようになる`　＝　処理結果を値として返す。
>
> > 関数で値を返してあげると、ほかの計算に使うことができるようになる

```JavaScript
function sum(a, b, c) {
  // console.log(a + b + c);
  return a + b + c;
  // return以降の記述は処理されない。
}

// sum(1, 2, 3);
// sum(3, 4, 5);

const total = sum(1, 2, 3) + sum(3, 4, 5); // 18
console.log(total);
```
## 18. ●**関数式を使う**
`関数を値として使いたい場合。`
>関数式を使う場合、関数を定数や変数に値として代入する形になる  
>>`変数に代入するような式のときは文末に ; （セミコロン）が必要`なので、少し注意しておいてください。  

![google](/img/const.png)
```JavaScript
'use strict';

// function sum(a, b, c) {
//   return a + b + c;
// }

const sum = function(a, b, c) {
  return a + b + c;
};

const total = sum(1, 2, 3) + sum(3, 4, 5);
console.log(total);
```
## 19. ●**アロー関数**
`関数式をより短く書くことのできる関数。`  
引数をひとつ渡すと倍にして返してくれる関数式を例に下に記述する。
>処理の中身が `return するだけの場合はもっと短く書くことができ`て、矢印の先に return する値を書いてあげればいい。  
>>"=>"　=　return
```JavaScript
'use strict';

// const sum = function(a, b, c) {
//   return a + b + c;
// };
const sum = (a, b, c) => a + b + c;
```
>アロー関数では`引数がひとつの場合、 () を省略できる`。
```JavaScript
'use strict';

// const double = function(a) {
//   return a * 2;
// };
const double = a => a * 2;
console.log(double(12));
```

## 20. ●**スコープについて理解する**
`スコープとは有効範囲という意味`  
>定数や変数がブロック内で宣言された場合、`その定数や変数はこのブロックの中でだけ有効 `というルールがある。  

>f() を実行したときは 1 が表示されているのですが、こちらの console.log(x) では f () の上で宣言した x が使われているので 2 になっているのがわかります。
>>スコープを理解していると、 `同じ定数名で違う値を表現できる`ようになります。
```JavaScript
'use strict';

const x = 2; //グローバルスコープ

function f() {
  const x = 1;
  console.log(x);
}

f(); // = 1
console.log(x); // = 2
```
## 21. ●**コードをブロックで囲う**
`コードがブロックで囲われていなければ、scriptタグを分けて記述しても、スコープが分かれるわけではない。`  
>JavaScript で複雑なコードを書くようになると、複数のスクリプトを読み込むことも多くなってきます。  
>そうした場合に今回見たようなエラーを防ぐには、`書いたコードはブロックで囲ってスコープを分ける、という習慣を付けておく`といいかと思います。

