目次
- [1. ●**DOMについて理解する**](#1-domについて理解する)
  - [1.1. ●**要素を操作する**](#11-要素を操作する)
  - [1.2. ●**複数の要素を取得する**](#12-複数の要素を取得する)
  - [1.3. ●**要素の取得方法を理解する**](#13-要素の取得方法を理解する)
  - [1.4. ●**クリックイベント,addEventListener()**](#14-クリックイベントaddeventlistener)
- [2. ●**要素の属性を操作する**](#2-要素の属性を操作する)
  - [2.1. ●**classNameを操作する**](#21-classnameを操作する)
  - [2.2. ●**classListを操作する**](#22-classlistを操作する)
  - [2.3. ●**カスタムデータ属性を扱う**](#23-カスタムデータ属性を扱う)
- [3. ●**要素を追加する**](#3-要素を追加する)
  - [3.1. ●**要素の複製,挿入**](#31-要素の複製挿入)
  - [3.2. ●**要素の削除をする**](#32-要素の削除をする)
- [4. ●**input要素を操作する**](#4-input要素を操作する)
  - [4.1. ●**セレクトボックスを操作する**](#41-セレクトボックスを操作する)
  - [4.2. ●**ラジオボタンを操作する**](#42-ラジオボタンを操作する)
  - [4.3. ●**チェックボックスを操作する**](#43-チェックボックスを操作する)
- [5. ●**その他のイベント**](#5-その他のイベント)
  - [5.1. ●**イベントオブジェクトを扱う**](#51-イベントオブジェクトを扱う)
  - [5.2. ●**フォームで使われるイベント**](#52-フォームで使われるイベント)
  - [5.3. ●**フォームを送信する**](#53-フォームを送信する)
  - [5.4. ●**イベントの伝播を理解する**](#54-イベントの伝播を理解する)
---

# 1. ●**DOMについて理解する**
>ブラウザですが、 HTML を読み込むと実は内部的に Document Object Model もしくは DOM と呼ばれるこういったデータ構造が作られて、`その内容に応じてページが描画がされる`、という仕組みになっています。  
そして、この `DOM を JavaScript で操作する`ことで様々な機能を作ることができます。  
JavaScript でアプリを作るには、こうした DOM 操作の知識が必要なので、これから詳しく見ていきましょう。

![google](/img/dom.png)
>それから、 `JavaScript が操作しているのは、あくまで DOM であって HTML のほうではない`点に注意しておきましょう。  
JavaScript で内容を書き換えたとしても、 HTML ファイルが書き換えられるわけではありません。

![google](/img/node.png)
>なお、ここでそれぞれのデータは Node と呼ばれていて、 document から始まってツリー状に枝分かれしているので、これを `Node ツリー、もしくは DOM ツリー`と言います。  
それから、 Node には種類はあって、 document と doctype は少し特殊なのですが、それ以外の HTML の要素を表す Node は要素 Node 、` Element Node` 、 Text や空白、もしくは改行は `Text Node `と呼ばれます。

![google](/img/sibling.png)
>それから、 Node 同士の関係には親子や兄弟といった用語をよく使います。  
また、こちらとこちらは同じ階層にあって兄弟関係にあるので、 `Sibling Node` と呼ばれます。

---
## 1.1. ●**要素を操作する**

```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <h1 id="target">ドットインストール</h1>
  <p>こんにちは。こんにちは。こんにちは。</p>
  <p>こんにちは。こんにちは。こんにちは。</p>
  <p>こんにちは。こんにちは。こんにちは。</p>

  <script src="js/main.js"></script>
</body>
</html>
```
>DOM は document という特殊なオブジェクトで扱うことができて、`文書内から特定の要素を取得する`には `querySelector() というメソッド`を使うことができます。

>`id を指定して要素を探す`には特殊なメソッドが用意されていて、 `getElementById() というメソッド`を使っても OK です。
```JavaScript
'use strict';

{
  function update() {
    // document.querySelector('h1').textContent = 'Changed!';
    // document.querySelector('#target').textContent = 'Changed!';
    document.getElementById('target').textContent = 'Changed!';
  }

  setTimeout(update, 1000);
}
```
## 1.2. ●**複数の要素を取得する**
>`querySelector() はこのセレクターで見つかった要素のうち最初のものだけしか取得できない`。  
そうではなくて、 document にある全ての要素を取得したい場合は、こちらを querySelector`All()` としてあげる必要があります。

>DOM で要素を取得する方法はいろいろありますが、 i`d 属性が付いていたら getElementById()` 、` id 属性がなければ querySelector() か querySelectorAll()` を使ってあげると良いでしょう。
```JavaScript
'use strict';

{
  function update() {
    document.getElementById('target').textContent = 'Changed!';
    document.querySelector('p').textContent = 'Changed!';
    document.querySelectorAll('p')[1].textContent = 'Changed!';
//配列と同じような記法が使えるので、 2 番目の要素を書き換えたかったら、その index は 1 番目なのでこのようにしてあげれば良いでしょう。

    document.querySelectorAll('p').forEach((p, index) => {
      p.textContent = `${index}番目のpです！`;
    });
  }

  setTimeout(update, 1000);
}
```
>それから、`全ての要素を処理したい`場合、 querySelectorAll() で取得した値には `forEach()` を使うことができます。  
では forEach() の復習になりますが、何番目の p かも表示したい場合は 2 つの引数を与えてあげれば良いですね。  
では、それぞれの要素を p 、そしてその順番を index として、こちらで p.textContent を書き換えていきましょう。

## 1.3. ●**要素の取得方法を理解する**
![google](/img/query.png)

![google](/img/li_sibling.png)

## 1.4. ●**クリックイベント,addEventListener()**
`クリックしたときの処理を指定することができるイベント`
>こちらのメソッドですが、第 1 引数にイベントの種類を文字列で渡してあげます。  
そのうえで click した時に実行したい処理を、こちらに関数で渡してあげます。(アロー関数で入れられている)
```JavaScript
'use strict';

{ 
  document.querySelector('button').addEventListener('click', () => {
    document.getElementById('target').textContent = 'Changed!';
  });
}
```
![google](/img/addEventListener.png)
# 2. ●**要素の属性を操作する**

![google](/img/henkamae.png)
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <button>Run</button>

  <h1 id="target" title="見出しです！">ドットインストール</h1>
  <p>こんにちは。こんにちは。こんにちは。</p>
  <p>こんにちは。こんにちは。こんにちは。</p>
  <p>こんにちは。こんにちは。こんにちは。</p>

  <script src="js/main.js"></script>
</body>
</html>
```
![google](/img/henkago.png)
>たとえば、背景色を設定したい場合、 background-color = skyblue ではなくて、 JavaScript から扱いときは - を消して、 2 単語目以降の最初の文字を大文字にしてあげる必要があります。
```JavaScript
'use strict';

{ 
  document.querySelector('button').addEventListener('click', () => {
    const targetNode = document.getElementById('target');

    targetNode.textContent = 'Changed!';
    targetNode.title = 'This is title!';
    targetNode.style.color = 'red';
    targetNode.style.backgroundColor = 'skyblue';
  });
}
```
>ただ、スタイルに関しては、 JavaScript でこのように書いてしまうと、 CSS との役割分担があいまいになるので、`見た目の指定は CSS に任せて、 `JavaScript では `class 属性の操作だけを書く`方法が一般的です。
## 2.1. ●**classNameを操作する**

```JavaScript

```
## 2.2. ●**classListを操作する**
`ボタンを押すごとに処理が入れ替わる`/on,offのような機能
>今回は、クリックするたびに my-color が付いたり外れたりする

>class 属性の操作ですが、 classList というプロパティを使ってあげると便利です。
```JavaScript
'use strict';

{ 
  document.querySelector('button').addEventListener('click', () => {
    const targetNode = document.getElementById('target');

    // targetNode.className = 'my-color my-border';
    // targetNode.classList.add('my-color');

//このクラスが付いてるかどうかを true 、 false で返してくれるので、条件分岐を使って my-color が付いていたら外すという処理を書いてみましょう。
    // if (targetNode.classList.contains('my-color') === true) {
// クラスを外すには、 classList.remove() を使ってあげます。
    //   targetNode.classList.remove('my-color');
    // } else {
// では、さらに my-color クラスが付いてなかったら付ける、という処理も else につないで書いてあげましょう。
    //   targetNode.classList.add('my-color');
    // }

    targetNode.classList.toggle('my-color');
  });
}
```
>こういった処理はよく書くのでもっと短い命令も用意されていたりします。  
どうするかというと、 `targetNode に対して classList.toggle('my-color')` としてあげると、上(コメント)と全く同じ意味になります。
## 2.3. ●**カスタムデータ属性を扱う**
>さて次ですが、 Run ボタンをクリックしたら h1 の英訳が表示されるようにしてみましょう。

>HTML では、 data- から始まっていれば独自の属性を付けられるので、 data-translation 属性を作ってあげて、値を Dotinstall にしてあげましょう。
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <button>Run</button>
  
  <h1 id="target" data-translation="Dotinstall">ドットインストール</h1>
  <p>こんにちは。こんにちは。こんにちは。</p>
  <p>こんにちは。こんにちは。こんにちは。</p>
  <p>こんにちは。こんにちは。こんにちは。</p>

  <script src="js/main.js"></script>
</body>
</html>
```
>こちらの値にアクセスするには、同名のプロパティである data-translation とすれば良いかと思いきや、クラス属性とカスタムデータ属性だけは例外的に違う書き方になります。
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const targetNode = document.getElementById('target');

      // targetNode.textContent = 'Dotinstall';
      targetNode.textContent = targetNode.dataset.translation;
  });
}
```
# 3. ●**要素を追加する**

![google](/img/domtree.png)
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <button>Run</button>
  
  <ul>
    <li>item 0</li>
    <li>item 1</li>
  </ul>

  <script src="js/main.js"></script>
</body>
</html>
```

```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const item2 = document.createElement('li');
    item2.textContent = 'item 2';
// ただ、これだけだと空の要素ができただけなので、 textContent を使って中身のテキストを設定してあげましょう。

    // const ulNode = document.querySelector('ul');
    const ul = document.querySelector('ul');
    ul.appendChild(item2);
  });
}
```
## 3.1. ●**要素の複製,挿入**
>次は要素を複製して DOM に追加する方法を見ていきましょう。

![google](/img/yousohukusei.png)
>その場合なのですが、親要素から見て、こちらの要素をこの要素の前に挿入するといった手法を使っていく
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const item0 = document.querySelectorAll('li')[0];
    const copy = item0.cloneNode(true);
    // なお、ここで false を渡すと要素の中身を複製しないことになるので空の li 要素が作られます。

    const ul = document.querySelector('ul');
    const item2 = document.querySelectorAll('li')[2];
    // そのうえでどうするかというと、親要素に対して insertBefore() というメソッドを使って copy を item2 の前に挿入してね、と書いてあげます。
    ul.insertBefore(copy, item2);
  });
}
```
## 3.2. ●**要素の削除をする**

```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const item1 = document.querySelectorAll('li')[1];

    // item1.remove();
    // 親Node.removeChild(削除するNode)
    document.querySelector('ul').removeChild(item1);
  });
}
```
# 4. ●**input要素を操作する**
>さて、次はユーザーから入力を受け取って要素を作ってみましょう。  
たとえば、入力部品があったとして、何かを入力してボタンをクリックしたら、下のリストに内容が追加されて、また違う内容を入力してボタンをクリックしたら、それがこちらに追加されるといったものを作ってみましょう。
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <input type="text">
  <button>Add</button>

  <ul>
  </ul>

  <script src="js/main.js"></script>
</body>
</html>
```
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const li = document.createElement('li');
    const text = document.querySelector('input');
    li.textContent = text.value;
    document.querySelector('ul').appendChild(li);

    text.value = '';
    text.focus();
  });
}
```

## 4.1. ●**セレクトボックスを操作する**
>では、ここから色を選んで、ボタンを押したら下のリストに追加される、といった機能を実装してみましょう。
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <select>
    <option value="red">赤</option>
    <option value="blue">青</option>
    <option value="yellow">黄</option>
  </select>
  <button>Add</button>

  <ul>
  </ul>

  <script src="js/main.js"></script>
</body>
</html>
```
>それから、 value の値にはタグの中身が使われるのですが、別の値にしたい場合は HTML のほうで value 属性を指定してあげれば OK です。
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const li = document.createElement('li');
    const color = document.querySelector('select');
    li.textContent = `${color.value} - ${color.selectedIndex}`;
    document.querySelector('ul').appendChild(li);
  });
}
```
## 4.2. ●**ラジオボタンを操作する**
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <input type="radio" name="color" value="red"> 赤
  <input type="radio" name="color" value="blue"> 青
  <input type="radio" name="color" value="yellow"> 黄
  <button>Add</button>

  <ul>
  </ul>
  <script src="js/main.js"></script>
</body>
</html>
```
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const colors = document.querySelectorAll('input');
    let selectedColor;

    colors.forEach(color => {
      if (color.checked === true) {
        selectedColor = color.value;
      }
    });

    const li = document.createElement('li');
    li.textContent = selectedColor;
    document.querySelector('ul').appendChild(li);
  });
}
```
## 4.3. ●**チェックボックスを操作する**

```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('click', () => {
    const colors = document.querySelectorAll('input');
    const selectedColors = [];

    colors.forEach(color => {
      if (color.checked === true) {
        selectedColors.push(color.value);
      }
    });
    // color の checked プロパティが true だったら selectedColors に追加したいので push() メソッドを使ってあげましょう。

    // あとは、前回と同じく li 要素を作って DOM ツリーに追加していきます。
    const li = document.createElement('li');
    // li 要素の textContent ですが、 selectedColors の配列の要素を , （カンマ）区切りで設定してあげましょう。
    // li.textContent = selectedColors.join(',');
    li.textContent = selectedColors;
    document.querySelector('ul').appendChild(li);
    // 配列は文字列で表現されるときに , 区切りになるので、 , 区切りの場合だったらこのように join() を書かなくても OK です。
  });
}
```
# 5. ●**その他のイベント**
- ダブルクリックイベント
- マウスムーブイベント
- キーダウンイベント（次項）
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('dblclick', () => {
    console.log('Double Clicked!');
  });

  document.addEventListener('mousemove', () => {
    console.log('moved!');
  });
}
```
## 5.1. ●**イベントオブジェクトを扱う**
- マウスカーソルの座標を取得
- キーダウンイベント

>こちらに前回書いたコードがありますが、実はこちらの関数に引数を渡せば、`ブラウザがイベントに関する情報をセットして渡してくれる`という仕組みになっています。  
なお、ここで渡される引数はイベントオブジェクトと呼ばれていて、慣習的に event の e がよく使われます。
```JavaScript
'use strict';

{
  document.querySelector('button').addEventListener('dblclick', () => {
    console.log('Double Clicked!');
  });

  document.addEventListener('mousemove', e => {
    // console.log('moved!');
    console.log(e.clientX, e.clientY);
  });

  document.addEventListener('keydown', e => {
    console.log(e.key);
  });
}
```
## 5.2. ●**フォームで使われるイベント**
- focus
  - フォーカスが当たったときのイベント
- blur
  - フォーカスが外れた時のイベント
- input
  - 内容が更新された時のイベント
- change
  - 更新が確定した時のイベント
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <textarea></textarea>

  <script src="js/main.js"></script>
</body>
</html>
```
```JavaScript
'use strict';

{
  const text = document.querySelector('textarea');

  text.addEventListener('focus', () => {
    console.log('focus');
  });

  text.addEventListener('blur', () => {
    console.log('blur');
  });
//クリックしてフォーカスが当たると focus と出ていますし、他のところをクリックしてフォーカスを外すと blur と出ているので OK そうです。

  text.addEventListener('input', () => {
    // console.log('input');
    console.log(text.value.length);
  });

  text.addEventListener('change', () => {
    console.log('change');
  });
}
// では、リロードして文字を入力するたびに input イベントが呼ばれていて、入力をおえてフォーカスを外してあげると change イベントがちゃんと呼ばれています。
```
## 5.3. ●**フォームを送信する**

```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
</head>
<body>
  <form>
    <input type="text">
    <button>Post</button>
  </form>

  <script src="js/main.js"></script>
</body>
</html>
```
```JavaScript
'use strict';

{
  document.querySelector('form').addEventListener('submit', e => {
    e.preventDefault();
    console.log('submit');
  });
}
```
## 5.4. ●**イベントの伝播を理解する**
![google](/img/denpa.png)
>この場合、たとえばこちらで click などのイベントが発生した場合、`そのイベントは親要素をたどってどんどん伝播していく`という仕組みになっています。  
これがなぜ便利かですが、たとえばこちらの全ての要素にイベントを追加したかったとします。  
その場合、全ての要素に追加しても良いのですが、`こちらの click は親にも伝播されるので、ここでのみ EventListener を追加してあげても OK` です。  

>また、 Event オブジェクトを使えば`クリックした要素は e.target` 、そして `EventListener を追加した要素は e.currentTarget で取得できる`ので、処理の中でこうしたプロパティを使うこともできます。
```HTML
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>JavaScript Basics</title>
  <style>
    li {
      cursor: pointer;
    }
    li.done {
      text-decoration: line-through;
    }
  </style>
</head>
<body>
  <ul> <!-- e.currentTarget -->
    <li>Todo</li>
    <li>Todo</li> <!-- e.target -->
    <li>Todo</li>
  </ul>

  <script src="js/main.js"></script>
</body>
</html>
```
>では今回、個々の li にイベントを設定するのではなくて、 `ul のほうに設定してみます`。  
そのうえで、先ほどのスライドで見たとおり、実際にクリックされた要素は Event オブジェクトの target 、`今回 EventListener を設定した ul 要素のほうは e.currentTarget で取得できる`ので、今回の場合は e.target のほうのクラスを付け替えてあげれば良いでしょう。  
したがって、 Event オブジェクトを渡してあげて、 e.target が li か一応判定しておきましょう。
```JavaScript
'use strict';

{
  document.querySelector('ul').addEventListener('click', e => {
    if (e.target.nodeName === 'LI') {
      e.target.classList.toggle('done');
    }
  });
}
```
