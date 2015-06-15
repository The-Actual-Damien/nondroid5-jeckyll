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


## デザインパターンを採用していないソースコードの例

### クラス名:SortableData

```Java
/* chap2/SortableData.java */
/* 非デザインパターン */
package chap2;

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

### クラス名:Sorter

```Java
/* chap2/Sorter.java */
/* 非デザインパターン */
package chap2;

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

### クラス名:SortTester

```Java
/* chap2/SortTester.java */
/* 非デザインパターン */
/* 実行クラス */
package chap2;

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

## 「Command」パターンによるソースコードの改良の例

### クラス名:SortableData

```Java
/* chap2/SortableData.java */
/* デザインパターン */
/* Commandパターンによる改良 */
package chap2;

/*ソート可能なデータクラス用のインターフェース*/
public interface SortableData {
	public int getSortKey();
}
```

### クラス名:Sorter

```Java
/* chap2/Sorter.java */
/* デザインパターン */
/* Commandパターンによる改良 */
package chap2;

public class Sorter {
	private SortableData[] target;
	private int num;
	
	public Sorter(SortableData [] in){
		target = in;
		num = target.length;
	}
	
	public SortableData[] sort( ){
		/*バブルソート*/
		for(int i = 0; i < num -1; i++){
			for(int j = i + 1; j < num; j ++){
				if( target[i].getSortKey() > (target[j]).getSortKey() ){
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

### クラス名:MyData

```Java
/* chap2/MyData.java */
/* デザインパターン */
/* Commandパターンによる改良 */
package chap2;

/* ソート可能な具象データクラス */
public class MyData implements SortableData {
	private String name;   /* 表示名 */
	private int value;   /* ソートされるべき値 */
	
	/* コンストラクタ */
	public MyData(String n,int v) {
		name = n; value = v;
	}
	
	/* ゲッタ */
	public String getName() { return name; }
	public int getValue() { return value; }
	
	/* SortableData　インターフェースが要求する */
	public int getSortKey() {return value;}
	
	/* 表示用のインターフェースだけ作っておく */
	public String toString() {
		return name + " " + value;
	}
}
```

### クラス名:MyNewData

```Java
/* chap2/MyNewData.java */
/* デザインパターン */
/* Commandパターンによる改良 */
package chap2;

/* ソート可能な具象データクラス */
public class MyNewData extends MyData {
	/*すでに SortableDta は implements　済み*/
	private int newValue;/*新規追加メンバ。これが新しくソートされるべき値になる。*/
	
	/* コンストラクタ */
	public MyNewData(String n,int v1, int v2) {
		super(n, v1);
		newValue = v2;
	}
	
	/* ゲッタ */
	public int getNewValue() { return newValue; }
	
	/* SortableData　インターフェースが要求する. 
	 * 規定クラスのものを上書きする.
	 */
	public int getSortKey() {return newValue;}
	
	/* 表示用のインターフェースだけ作っておく .
	 *これも基底クラスのものを上書き. 
	 */
	public String toString() {
		String ret = super.toString(); /*親クラスの同名メソッドを呼び出す*/
		return ret + " " + newValue; /*それに追加*/
	}
}
```

### クラス名:Value1Select

```Java
/* chap2/Value1Select.java */
/* デザインパターン */
/* Commandパターンによる改良 */
package chap2;

/* ソートキーとして、MyNewData.valueを使う　Command　オブジェクト */
public class Value1Select implements SortableData{
	private MyNewData data; /*データを保持*/
	
	public Value1Select (MyNewData mnd){
		data = mnd;
	}

	/*Interface で定められてた getSortKey() で　value　を選ぶ*/
	public int getSortKey(){
		return data.getValue();
	}
	
	/* 出力は MyNewDataに任せる */
	public String toString(){
		return data.toString();
	}
}
```

### クラス名:Value2Select

```Java
/* chap2/Value2Select.java */
/* デザインパターン */
/* Commandパターンによる改良 */
package chap2;

/* ソートキーとして、MyNewData.newValueを使う　Command　オブジェクト */
public class Value2Select implements SortableData{
	private MyNewData data; /*データを保持*/
	
	public Value2Select (MyNewData mnd){
		data = mnd;
	}

	/*Interface で定められてた getSortKey() で　newValue　を選ぶ*/
	public int getSortKey(){
		return data.getNewValue();
	}
	
	/* 出力は MyNewDataに任せる */
	public String toString(){
		return data.toString();
	}
}
```

### クラス名:SortTester1

```Java
/* chap2/SortTester1.java */
/* デザインパターン */
/* Commandパターンによる改良 */
/* 実行クラス */
package chap2;

public class SortTester1 {
	private SortableData [] data = {
		new MyData( "test0", 100 ),
		new MyData( "test1", 73 ),
		new MyData( "test2", 34 ),
		new MyData( "test3", 11 ),
		new MyData( "test4", 98 ),
		new MyData( "test5", 54 ),
		new MyData( "test6", 3 )
	};
	
	public static void main(String[] args){
		new SortTester1();
	}
	public SortTester1() {
		Sorter sorter = new Sorter( data );
		SortableData [] result = sorter.sort();
		for(int i = 0; i < result.length; i++){
			System.out.println( result[i] );
		}
	}
}
```

### クラス名:SortTester2

```Java
/* chap2/SortTester2.java */
/* デザインパターン */
/* Commandパターンによる改良 */
/* 実行クラス */
package chap2;

public class SortTester2 {
	private SortableData [] data = {
		new MyNewData( "test0", 100, 43 ),
		new MyNewData( "test1", 73, 11 ),
		new MyNewData( "test2", 34, 39 ),
		new MyNewData( "test3", 11, 75 ),
		new MyNewData( "test4", 98, 3 ),
		new MyNewData( "test5", 54, 81 ),
		new MyNewData( "test6", 3, 56 )
	};
	
	public static void main(String[] args){
		new SortTester2();
	}
	public SortTester2() {
		Sorter sorter = new Sorter( data );
		SortableData [] result = sorter.sort();
		for(int i = 0; i < result.length; i++){
			System.out.println( result[i] );
		}
	}
}
```

### クラス名:SortTester3

```Java
/* chap2/SortTester3.java */
/* デザインパターン */
/* Commandパターンによる改良 */
/* 実行クラス */
/* ValueSelectを使用した入力値の選択 */
package chap2;

public class SortTester3 {
	private SortableData [] data = {
		new Value1Select( new MyNewData( "test0", 100, 43 ) ),
		new Value1Select( new MyNewData( "test1", 73, 11 ) ),
		new Value1Select( new MyNewData( "test2", 34, 39 ) ),
		new Value1Select( new MyNewData( "test3", 11, 75 ) ),
		new Value1Select( new MyNewData( "test4", 98, 3 ) ),
		new Value1Select( new MyNewData( "test5", 54, 81 ) ),
		new Value1Select( new MyNewData( "test6", 3, 56 ) )
	};
	
	public static void main(String[] args){
		new SortTester3();
	}
	public SortTester3() {
		Sorter sorter = new Sorter( data );
		SortableData [] result = sorter.sort();
		for(int i = 0; i < result.length; i++){
			System.out.println( result[i] );
		}
	}
}
```
