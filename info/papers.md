# 読んだ論文
これまで読んだ論文をまとめる

## [Revisiting Test Cases to Boost Generate-and-Validate Program Repair](https://www.darkrsw.net/papers/ICSME2021.pdf)(ICSME'21)
欠陥限局に用いるテストケースそのものに対する洞察を行っていた。
普段から使ってるDefects4jに格納されたプロジェクトのバグをAPRが修正するにあたって、どんなバグがチャレンジングなのかを統計的にまとめてくれているので研究のモチベーションとしては良かった。

## [Refining Fitness Functions in Test-Based Program Repair](http://www0.cs.ucl.ac.uk/staff/a.blot/files/bian_apr-icse_2021.pdf)(ICSEW'21)
動機: 失敗テストの予測値と実測値の差分をデータ化してそのデータをフィットネス関数に埋め込みAPRの性能を上げたい！
結論: 数値的距離を用いたフィットネス関数を用いても従来手法(GenProg, ARJAe)に比べて優位な差は見られなかった。
ワークショップの論文で8ページなので軽い読み物としては良かった。
- 研究するにあたってGinという遺伝的アルゴリズムを用いたAPRのフレームワークを使っていた
    - 既存のツールに比べてミューテーションに用いる演算子が豊富らしい
- 筆者らが拡張したテストケースがQuixBugsのベンチマークに追加されたらしい(研究の副産物)
- 失敗テストの数値的距離をフィットネス関数に用いれるようにデータ加工する手法のアイデアは面白かった
    - 妥当性があるかどうかはともかく
- [別に読んだ論文](https://www.darkrsw.net/papers/ICSME2021.pdf)だと、バグの内訳では異なる値を出力することによるエラー比率が70%もあったので、研究の意義としては大きいのかも