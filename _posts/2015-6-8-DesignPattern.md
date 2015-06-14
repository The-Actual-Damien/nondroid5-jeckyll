---
layout: post
title: デザインパターンに関して
---

今更ながら、GoFに関して学習している。

GoFとは、「The Gang Of Four」で4人の奴らという意味である。

4人とは、エリック・ガンマ、リチャードヘルム、ラルフ・ジョンソン、

ジョン・ブリディースらのことを指している。

これは様々なプログラムで再利用できる汎用的な設計パターンのことです。

GoFデザインパターンは全部で23種類ある。

学習することで強力なツールになるとのことです。

メリット①　「オブジェクト指向設計」がしっかりと身に付く

メリット②　再利用性が向上する

メリット③　結合性が下がり、保守改善がしやすくなる

メリット④　クラス設計を意識的に捉える習慣が付く

メリット⑤　センスの良いテクニックを覚えれる

メリット⑥　プログラマ同士の共通の語彙として使える

覚え方は以下のように覚えると良いらしい

|            |                       生成                        |      構造      |           振る舞い           |
|:----------:|:-------------------------------------------------:|:--------------:|:----------------------------:|
|   クラス   |                   FactoryMethod                   |Adapter (Class)           |Interpreter<br/>TemplateMethod|
|オブジェクト|AbstractFactory<br/>Builder<br/>Prototype Singleton|Adapter(Object)<br/>Bridge<br/>Composite<br/>Decorator<br/>Decorator<br/>Flyweight<br/>Proxy|Chainof Responsibility <br/>Command<br/>Iterator<br/>Mediator</br>Memento<br/>Observer<br/>State<br/>Strategy</br>Visitor|

「Command」

- Command入力の変更に対応

「Factory Method」

- メソッドの追加に対応

「Simple Factory(Bulder)」

- 動的ローディングに対応

「Template Method」

- 抽象基底クラス(クラス生成の抽象化に対応)

