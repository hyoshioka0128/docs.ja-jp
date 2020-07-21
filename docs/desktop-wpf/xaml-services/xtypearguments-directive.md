---
title: x:TypeArguments ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- x:TypeArguments
- xTypeArguments
- TypeArguments
helpviewer_keywords:
- x:TypeArguments attribute [XAML Services]
- TypeArguments attribute in XAML [XAML Services]
- XAML [XAML Services], x:TypeArguments attribute
ms.assetid: 86561058-d393-4a44-b5c3-993a4513ea74
ms.openlocfilehash: 69da9329f140121b66c71d4cf2e99e9d14a1b207
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432630"
---
# <a name="xtypearguments-directive"></a>x:TypeArguments ディレクティブ

ジェネリック型の制約型引数をジェネリック型のコンストラクターに渡します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:TypeArguments="typeString" .../>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`object`|CLR ジェネリック型によってサポートされる XAML 型のオブジェクト要素宣言。 既定`object`の XAML 名前空間からでない XAML 型を参照する`object`場合は、存在する XAML`object`名前空間を示すプレフィックスが必要です。|
|`typeString`|1 つ以上の XAML 型名を文字列として宣言する文字列。 構文に関するその他の注意事項については、「解説」を参照してください。|

## <a name="remarks"></a>解説

ほとんどの場合、`typeString`文字列内の情報項目として使用される XAML 型にはプレフィックスが付けられます。 CLR の一般的な制約 (たとえば<xref:System.Int32><xref:System.String>、 ) の型は、CLR 基本クラス ライブラリから取得されます。 これらのライブラリは、フレームワーク固有の一般的な既定の XAML 名前空間にはマップされないため、XAML の使用に対するプレフィックス マッピングが必要です。

コンマ区切り記号を使用して、複数の XAML 型名を指定できます。

ジェネリック制約自体がジェネリック型を使用する場合、入れ子になった制約型引数は括弧 () で囲むことができます。

この定義`x:TypeArguments`は.NET XAML サービスに固有で、CLR バッキングを使用していることに注意してください。 言語レベルの定義は、 [ \[MS-XAML\]セクション 5.3.11](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))にあります。

## <a name="usage-examples"></a>使用例

これらの例では、次の XAML 名前空間定義が宣言されていると仮定します。

```xaml
xmlns:sys="clr-namespace:System;assembly=mscorlib"
xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"
```

### <a name="liststring"></a>リスト\<文字列>

`<scg:List x:TypeArguments="sys:String" ...>`型引数を使用<xref:System.Collections.Generic.List%601>して<xref:System.String>new をインスタンス化します。

### <a name="dictionarystringstring"></a>辞書\<文字列,文字列>

`<scg:Dictionary x:TypeArguments="sys:String,sys:String" ...>`2 つの型<xref:System.Collections.Generic.Dictionary%602>引数を<xref:System.String>使用して new をインスタンス化します。

### <a name="queuekeyvaluepairstringstring"></a>キュー<キー\<値ペア文字列,文字列>>

`<scg:Queue x:TypeArguments="scg:KeyValuePair(sys:String,sys:String)" ...>`内部制約型の<xref:System.Collections.Generic.Queue%601>引数<xref:System.Collections.Generic.KeyValuePair%602><xref:System.String>と での制約を持つ新しいを<xref:System.String>インスタンス化します。

## <a name="xaml-2006-and-wpf-generic-xaml-usages"></a>XAML 2006 および WPF の汎用 XAML の使用法

XAML 2006 の使用法および WPF アプリケーションで使用される XAML の場合`x:TypeArguments`、XAML でのジェネリック型の使用方法には次の制限事項と、一般的なジェネリック型の使用が適用されます。

- ジェネリック型を参照する汎用 XAML の使用法をサポートできるのは、XAML ファイルのルート要素だけです。

- ルート要素は、少なくとも 1 つの型引数を持つジェネリック型にマップする必要があります。 たとえば <xref:System.Windows.Navigation.PageFunction%601> です。 ページ関数は、WPF での XAML 汎用の使用サポートの主なシナリオです。

- ジェネリックのルート要素 XAML オブジェクト要素も、 を使用して`x:Class`部分クラスを宣言する必要があります。 これは、WPF ビルド アクションを定義する場合にも当てはまります。

- `x:TypeArguments`ネストされたジェネリック制約を参照できません。

## <a name="xaml-2009-or-xaml-2006-with-no-wpf-30-or-wpf-35-dependency"></a>WPF 3.0 または WPF 3.5 の依存関係がない XAML 2009 または XAML 2006

XAML 2006 または XAML 2009 の .NET XAML サービスでは、汎用 XAML の使用に関する WPF 関連の制限が緩和されました。 XAML マークアップ内の任意の位置で、バッキング型システムとオブジェクト モデルでサポートできる汎用オブジェクト要素をインスタンス化できます。

共通言語プリミティブの XAML 型を取得するために CLR 基本型をマッピングする代わりに XAML 2009 を使用する場合は、[共通 XAML 言語プリミティブの組み込み型を](types-for-primitives.md)`typeString`情報項目として使用できます。 たとえば、次のように宣言できます (プレフィックス マッピングは表示されませんが、x は XAML 2009 の XAML 言語 XAML 名前空間です)。

```xaml
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>
```

WPF で 、.NET Framework 4 または .NET Core 3.0 以降を対象とする場合は、XAML `x:TypeArguments` 2009 の機能を緩い XAML (マークアップ コンパイルされていない XAML) と共に使用できます。 WPF 向けにマークアップ コンパイルされた XAML、および XAML の BAML 形式は、現在、XAML 2009 のキーワードと機能をサポートしていません。 XAML をマークアップ コンパイルする必要がある場合は[、XAML 2006 および WPF 汎用 XAML の使用方法](#xaml-2006-and-wpf-generic-xaml-usages)に関するセクションに記載されている制限の下で操作する必要があります。 BAML は .NET フレームワークでのみサポートされています。

## <a name="see-also"></a>関連項目

- [x:Class ディレクティブ](xclass-directive.md)
- [x:Type マークアップ拡張機能](xtype-markup-extension.md)
- [共通の XAML 言語プリミティブの組み込み型](types-for-primitives.md)
- [XAML のジェネリック](generics.md)
