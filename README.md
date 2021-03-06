# code-inspection
設計の改善課題を、コードのメトリクスから発見する

## 概要

Javaの設計（クラス、メソッド、パッケージ）の改善課題を発見するための、測定指標のガイドライン。

使用ツール：IntelliJ IDEA の Code Inspection

## メソッド

指標 | 英語名 | ガイドライン<br>(デフォルト値) | 説明 
--|--|:-------:|--
複雑度|overly complex method|2 (10)|分岐の複雑さ。if文、for文、そのネストが多いほど複雑になる。<br>リファクタリングの候補。
結合度|overly coupled method|2 (10)| メソッド内で使う他のクラスの数。<br>他のクラスへの依存が多いほど密結合になる。
長さ|overly long method|5 (30)|長いメソッドほど異なる関心事が混在している。<br>メソッド抽出の候補。
ネストの深さ|overly nested method|1 (5)|ネストの深さは、異なるレベルの関心事が混在。<br>メソッド抽出の候補。
多重ループ|method with multiple loop| | 多重ループは、異なるレベルの関心事が混在している。<br>メソッド抽出の候補。
メソッドの引数|method with too many parameters|2 (5)|パラメータが多いほど、コードが複雑になる。<br>パラメータクラスの抽出の候補。
コンストラクタの引数|constructor with too many parameters|3 (5)|複雑なコンストラクタは、意図が不明確で使う側の負担になる。<br>クラスの分割の候補。

### 引数の数

メソッドが使う第一のデータは、インスタンス変数になる。  
オブジェクト指向のメソッドに渡す引数は、手続き型のサーブルーチンに渡す引数よりも少なくなる。

インスタンス変数だけで、判断／加工／計算ができるロジックを記述したメソッドであれば、引数はゼロ。  
インスタンス変数に他のデータを組合せて判断／加工／計算する場合、原則として一つだけのデータを対象にする。  
引数の用途がオプション（振る舞いの条件分岐）の場合は、目的別にメソッドを分けるか多態を検討する。

コンストラクタに多くの引数を渡すのは、インスタンス変数が多い。  
インスタンス変数が多いクラスは、異なる関心事が混在している可能性が高い。  
クラスの分割を検討する。

## クラス

指標 | 英語名 | ガイドライン<br>(デフォルト値) | 説明 
--|--|:-------:|--
複雑度|overly complex class|20 (80)|メソッドの複雑度の合計。
結合度|overly coupled class|5 (15)|他のクラスに依存する度合い。
フィールドの数|too many fields|3 (10)|フィールド（インスタンス変数）の数。<br>関心の分離の改善の候補。
メソッドの数|too many methods|7 (20)|人間が一度が理解できる個数は７個が限度。
コンストラクタの数|too many constructors|2 (5)|コンストラクタの多重定義は、わかりにくい。<br>完全コンストラクタ＋デフォルトの２つがガイドライン。

### フィールドの数

クラスは、判断／加工／計算のロジックの置き場所。  
フィールド（インスタンス変数）は、その計算の対象となるデータ。  
フィールドの数が多い場合は、異なる関心事が混在している可能性が高い。  
クラスの分割の候補。

なお、ロジックをほとんど持たないデータの入れ物クラスは、このガイドラインの対象外。  
このガイドラインは「ロジックの整理の手段」としてのクラス設計の改善のガイドライン。

## パッケージ

指標 | 英語名 | ガイドライン<br>(デフォルト値) | 説明 
--|--|:-------:|--
少ないクラス|pacakge with too few classes|3 (3)|クラス数が少なすぎる。<br>他のパッケージとの統合の候補。
多すぎるクラス|package with too many classes|10 (10)|クラス数が多すぎる。<br>パッケージ分割の候補。
孤立したクラス|class indepedent of its package||パッケージ内から使われない、かつ、パッケージの他のクラスを使わない。<br>このパッケージに存在することが疑わしい。
特定のパッケージだけから使う|class only used from one other package||特定のパッケージだけから使う。<br>そのパッケージへの移動の候補。

