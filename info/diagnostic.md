# Diagnostic

Javaにおいて、なんらかの実行結果についての詳細な情報を格納してくれるクラスです。

- [JCDiagnostic](https://java-browser.yawk.at/java/13/jdk.compiler/com/sun/tools/javac/util/JCDiagnostic.java#com.sun.tools.javac.util.JCDiagnostic.DiagnosticInfo) : Diagnosticを継承したクラス. javacの実行結果をまとめてくれる. メソッドの使い方や概要は[こちら](https://www.javadoc.io/doc/org.kohsuke.sorcerer/sorcerer-javac/latest/com/sun/tools/javac/util/JCDiagnostic.html)を参照. 
    - なお、これを使おうとすると、なぜか「名前のないモジュールにエクスポートされていません」というエラーが出力された. 解決はまだしていないので、詳細が分かる方は是非連絡をお願いします! 