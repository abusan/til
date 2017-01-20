# .onの使い方(jQuery 3)

jQuery 1.7からイベントのバインドのためにonメソッドが追加されました。  
古いjQueryで動いていたソースをjQuery 3.1.1で動くように修正する作業でonメソッドについて詳しく調べたところ、なかなか面白い使い方ができるのでまとめます。  

## 基本

```javascript
$('#id').on('click', function(){
    alert('click!');
});
```
その名の通り基本形。古いコードでliveがそこら中に使われていても置換すれば大丈夫なんです。  

## セレクターで指定
セレクターを指定してイベントを登録できます。

```javascript
$('#table').on('click', 'tr', function(){
    alert('click!');
});
```

```javascript
$('#table tr').on('click', function(){
    alert('click!');
});
```

上記の2つは同じようにイベントを登録できます。いまいち使いどころがわからない。  

## 同じ要素に複数のイベントを登録
例えば一つの要素にclickとhoverの二つのイベントを実装することがあるかもしれない。  

```javascript
$('#id').on(
    {
        click: function(){
            alert('click!');
        },
        mouseenter: function(){
            alert('hover!');
        },
        mouseleave: function(){
            alert('unhover!');
        }
    }
);
```

オブジェクトに複数入れると全部登録してくれます。賢いですね。
hoverはmouseenterとmouseleaveなんですね。知らなかった……  

## event.dataで値を渡すことができる
第二引数にオブジェクトを渡してやると、コールバック関数に渡すことができます。  

```javascript
$('#id').on(
    'click',
    {
        id: 101,
        name: 'sanshirou'
    },
    function(event){
        alert(event.data.id + ':' + event.data.name);
    }
);
```
これでもうグローバル変数に値を入れておいてコールバックの中で使うとかいう石器時代のコードとは決別できますね！  

### triggerから値を渡す
登録したイベントはtriggerメソッドで呼び出すことができますが、triggerメソッドからでも値を渡すことができます。  

```javascript
$('#id').on('click', function(event){
    alert(event.name));
});

$('#id').trigger('click', { name: 'tarou' });
```

### triggerから配列で値を渡す
配列で値を渡すと、引数として扱われます。  

```javascript
$('#id').on('click', function(event, id, name){
    alert(id + ':' + name);
});

$('#id').trigger('click', [102, 'tarou']);
```

## イベントの伝播(バブリング)を止める
コールバックにfalseを渡すか、コールバックからfalseをreturnするとイベントの伝播を止めることができます。  

```javascript
$('#form').on('submit', false );
```

```javascript
$('#form').on('submit', function(){
    return false;
});
```

```javascript
$('#form').on('submit', function(event){
    event.preventDefault();
    event.stopPropagation();
});
```

デフォルト挙動と伝播の両方を止めたいならreturn falseでOKですが、伝播を止めたくないなら素直にpreventDefault呼びましょうねってことですね。  
