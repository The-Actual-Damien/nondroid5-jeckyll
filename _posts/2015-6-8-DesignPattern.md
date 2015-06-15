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

```Java
/* chap2.A/SortableData.java */
/* 非デザインパターン */
package chap2.A;

/*ソート対象となるデータのクラス*/
public class SortableData {
	public String name; /* 表示名 */
	public int value; /*ソートされるべき値*/
	
	public SortableData(String n, int v){
		name = n; value = v;
	}
	
	/*表示用のインターフェースだけ作っておく*/
	public String toString() {
		return name + " " + value;
	}
}
```

```Java
/* chap2.A/Sorter.java */
/* 非デザインパターン */
package chap2.A;

/* ソートを実行するクラス */
public class Sorter {
	private SortableData [] target;
	private int num;
	
	public Sorter(SortableData [] in ){
		target = in;
		num = target.length;
	}
	
	public SortableData [] sort(){
		/*バブルソート*/
		for(int i = 0; i < num -1; i++){
			for(int j = i + 1; j < num; j ++){
				if(target[i].value > target[j].value){
					SortableData tmp = target[i];
					target[i] = target[j];
					target[j] = tmp;
				}
			}
		}
		return target;
	}
}
```

```Java
/* chap2.A/SortTester.java */
/* 非デザインパターン */
package chap2.A;

public class SortTester {
	private SortableData [] data = {
		new SortableData( "test0", 100 ),
		new SortableData( "test1", 73 ),
		new SortableData( "test2", 34 ),
		new SortableData( "test3", 11 ),
		new SortableData( "test4", 98 ),
		new SortableData( "test5", 54 ),
		new SortableData( "test6", 3 )
	};
	
	public static void main(String[] args){
		new SortTester();
	}
	public SortTester() {
		Sorter sorter = new Sorter( data );
		SortableData [] result = sorter.sort();
		for(int i = 0; i < result.length; i++){
			System.out.println( result[i] );
		}
	}
}
```
