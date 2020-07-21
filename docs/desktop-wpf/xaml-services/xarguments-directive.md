---
title: x:Arguments ディレクティブ
ms.date: 03/30/2017
helpviewer_keywords:
- x:Arguments directive [XAML Services]
- Arguments directive in XAML [XAML Services]
- XAML [XAML Services], x:Arguments directive
ms.assetid: 87cc10b0-b610-4025-b6b0-ab27ca27c92e
ms.openlocfilehash: 5ec6e192688e1065ea847db6c175ad9da0e743fe
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432834"
---
# <a name="xarguments-directive"></a>x:Arguments ディレクティブ

XAML でのパラメーターなしのコンストラクター オブジェクト要素宣言、またはファクトリ メソッド オブジェクト宣言の構築引数をパッケージ化します。

## <a name="xaml-element-usage-nonparameterless-constructor"></a>XAML 要素の使用方法 (非パラメーターなしのコンストラクター)

```xaml
<object ...>
  <x:Arguments>
    oneOrMoreObjectElements
  </x:Arguments>
</object>
```

## <a name="xaml-element-usage-factory-method"></a>XAML 要素の使用方法 (ファクトリ メソッド)

```xaml
<object x:FactoryMethod="methodName"...>
  <x:Arguments>
    oneOrMoreObjectElements
  </x:Arguments>
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`oneOrMoreObjectElements`|バッキング非パラメーターのコンストラクターまたはファクトリ メソッドに渡す引数を指定する 1 つ以上のオブジェクト要素。<br /><br /> 一般的な使用方法は、オブジェクト要素内の初期化テキストを使用して、実際の引数値を指定することです。 「例」セクションを参照してください。<br /><br /> 要素の順序は重要です。 XAML 型は、バッキング コンストラクターまたはファクトリ メソッドのオーバーロードの型と型の順序と一致する必要があります。|
|`methodName`|引数`x:Arguments`を処理するファクトリ メソッドの名前。|

## <a name="dependencies"></a>依存関係

`x:FactoryMethod`適用される範囲と動作を`x:Arguments`変更できます。

no`x:FactoryMethod`を指定すると`x:Arguments`、バッキング コンストラクターの代替 (既定以外の) シグネチャに適用されます。

指定`x:FactoryMethod`した場合は`x:Arguments`、名前付きメソッドのオーバーロードに適用されます。

## <a name="remarks"></a>解説

XAML 2006 では、初期化テキストを使用して既定以外の初期化をサポートできます。 しかし、初期化テキスト構築技術の実用化は限られている。 初期化テキストは単一のテキスト文字列として扱われます。したがって、カスタム情報項目と文字列からのカスタム区切り記号を解析できる構築動作に対して型コンバーターが定義されていない限り、単一のパラメーター初期化の機能を追加するだけです。 また、オブジェクト ロジックへのテキスト文字列は、実際の文字列以外のプリミティブを処理するための、指定された XAML パーサーのネイティブな既定の型コンバーターである可能性があります。

XAML`x:Arguments`の使用法は、一般的な意味でのプロパティ要素の使用ではありません。 これは、マークアップが子コンテンツの既定以外の範囲`x:Code`として解釈される要素がマークされている場合など、他のディレクティブに似たものです。 この場合、各オブジェクト要素の XAML 型は、使用`x:Arguments`法で参照しようとしている特定のコンストラクター ファクトリ メソッド シグネチャを決定するために XAML パーサーによって使用される引数の型に関する情報を伝達します。

`x:Arguments`オブジェクト要素が構築される場合は、オブジェクト要素の他のプロパティ要素、コンテンツ、内部テキスト、または初期化文字列の前に置く必要があります。 内部`x:Arguments`のオブジェクト要素には、その XAML 型とそのバッキング コンストラクターまたはファクトリ メソッドで許可されている属性と初期化文字列を含めることができます。 オブジェクトまたは引数の場合、確立されたプレフィックス マッピングを参照することで、既定の XAML 名前空間の外部にあるカスタム XAML 型または XAML 型を指定できます。

XAML プロセッサは、次のガイドラインを使用して、 で`x:Arguments`指定した引数を使用してオブジェクトを構築する方法を決定します。 指定`x:FactoryMethod`した場合、情報は指定された`x:FactoryMethod`情報と比較されます (の値`x:FactoryMethod`はメソッド名であり、名前付きメソッドはオーバーロードを持つことができます)。 指定`x:FactoryMethod`しない場合、情報はオブジェクトのすべてのパブリック コンストラクター オーバーロードのセットと比較されます。 次に、XAML 処理ロジックはパラメーターの数を比較し、一致するアリティを持つオーバーロードを選択します。 複数の一致がある場合、XAML プロセッサは、指定されたオブジェクト要素の XAML 型に基づいてパラメーターの型を比較する必要があります。 一致が複数ある場合、XAML プロセッサの動作は未定義です。 が`x:FactoryMethod`指定されているが、メソッドを解決できない場合、XAML プロセッサは例外をスローする必要があります。

XAML 属性の`<x:Arguments>string</x:Arguments>`使用は技術的に可能です。 ただし、初期化テキストと型コンバーターを使用して実行できる機能以外の機能は提供されません。

## <a name="examples"></a>例

次の例では、パラメーターなしのコンストラクター シグネチャを示し、そのシグネチャ`x:Arguments`にアクセスする XAML の使用方法を示します。

```csharp
public class Food {
  private string _name;
  private Int32 _calories;
  public Food(string name, Int32 calories) {
      _name=name;
      _calories=calories;
  }
}
```

```xaml
<my:Food>
  <x:Arguments>
      <x:String>Apple</x:String>
      <x:Int32>150</x:Int32>
  </x:Arguments>
</my:Food>
```

次の例は、ターゲット ファクトリ メソッドシグネチャを示し、`x:Arguments`そのシグネチャにアクセスする XAML の使用方法を示しています。

```csharp
public Food TryLookupFood(string name)
{
switch (name) {
  case "Apple": return new Food("Apple",150);
  case "Chocolate": return new Food("Chocolate",200);
  case "Cheese": return new Food("Cheese", 450);
  default: {return new Food(name,0);
}
}
```

```xaml
<my:Food x:FactoryMethod="TryLookupFood">
  <x:Arguments>
      <x:String>Apple</x:String>
  </x:Arguments>
</my:Food>
```

## <a name="see-also"></a>関連項目

- [.NET XAML サービスで使用するカスタム型の定義](define-custom-types.md)
- [XAML の概要 (WPF)](../fundamentals/xaml.md)
