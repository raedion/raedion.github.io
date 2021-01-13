# その他
諸知識はこちらにおきます.

- [総称型の未検査キャスト](http://www.profaim.jp/lang-ref/java/generics/cast.php)
    - abstractlistのように、ジェネリクスを指定していないリスト構造を引数とするとき、各要素(element)がどんな型かわからず、Javaのコンパイラが警告をするため、これを防ぐための手法を載せる. 具体的には、
        1. @SuppressWarnings("unchecked") をメソッドのアノテーションとして追加
        2. 上記やりかただとメソッド全体が警告をしなくなってしまうから別のメソッドを用意しておくといいかも
```Java
/**
 * 変換メソッド
 * @param src 変換したい変数
 * @return キャストされた変数
 */ 
@SuppressWarnings("unchecked")
public <T> T autoCast(Object src) {
    T dst = (T) src;        // 変換元をキャスト
    return dst; 
}
```