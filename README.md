# code-inspection
設計の改善課題を、コードのメトリクスから発見する

## 概要

Javaの設計（クラス、メソッド、パッケージ）の改善課題を発見するための、測定指標のガイドライン。

使用ツール：IntelliJ IDEA の Code Inspection

## メソッド

指標 | 英語名 | ガイドライン<br>(デフォルト値) | 説明 
--|--|:--:|--
複雑性|overly complex method|2 (10)|分岐の複雑さ。if文、for文、そのネストが多いほど複雑になる。<br>リファクタリングの候補。
結合度|overly coupled method|2 (10)| メソッド内で使う他のクラスの数。<br>他のクラスへの依存が多いほど密結合になる。
長さ|overly long method|5 (30)|長いメソッドほど異なる関心事が混在している。<br>メソッド抽出の候補。
ネストの深さ|overly nested method|1 (5)|ネストの深さは、異なるレベルの関心事が混在。<br>メソッド抽出の候補。
多重ループ|method with multiple loop| | 多重ループは、異なるレベルの関心事が混在している。<br>メソッド抽出の候補。
メソッドの引数|method with too many parameters|2 (5)|パラメータが多いほど、コードが複雑になる。<br>パラメータクラスの抽出の候補。
コンストラクタの引数|constructor with too many parameters|3 (5)|複雑なコンストラクタは、意図が不明確で使う側の負担になる。<br>クラスの分割の候補。
