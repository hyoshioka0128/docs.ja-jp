---
title: x:Type マークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- x:TypeExtension
- Type
- x:Type
- xType
- TypeExtension
helpviewer_keywords:
- x:Type markup extension [XAML Services]
- XAML [XAML Services], x:Type markup extension
- XAML [XAML Services], TargetType attribute
- TargetType attribute [XAML Services]
- Type markup extension in XAML [XAML Services]
ms.assetid: e0e0ce6f-e873-49c7-8ad7-8b840eb353ec
ms.openlocfilehash: f75d4e30dc41bbce995e466466c96c1a2830949b
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432636"
---
# <a name="xtype-markup-extension"></a>x:Type マークアップ拡張機能

指定した<xref:System.Type>XAML 型の基になる型である CLR オブジェクトを提供します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object property="{x:Type prefix:typeNameValue}" .../>
```

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xaml
<x:Type TypeName="prefix:typeNameValue"/>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`prefix`|省略可能。 既定以外の XAML 名前空間をマップするプレフィックス。 プレフィックスを指定する必要がない場合は、多くの場合必要ありません。 「解説」を参照してください。|
|`typeNameValue`|必須。 現在の既定の XAML 名前空間に解決できる型名。または指定されたマップされたプレフィックス`prefix`(指定されている場合)|

## <a name="remarks"></a>解説

マークアップ`x:Type`拡張機能は、C# の`typeof()`演算子や、Visual Basic`GetType`の演算子と同様の関数を持っています。

マークアップ`x:Type`拡張機能は、型を取得するプロパティに対して文字列から変換する<xref:System.Type>動作を提供します。 入力は XAML 型です。 入力<xref:System.Type>XAML 型と出力 CLR の関係は、XAML<xref:System.Type>スキーマ<xref:System.Xaml.XamlType.UnderlyingType%2A>コンテキストと<xref:System.Xaml.XamlType>コンテキストが提供する<xref:System.Windows.Markup.IXamlTypeResolver>サービスに<xref:System.Xaml.XamlType>基づいて必要なを検索した後、出力が入力の .

NET XAML サービスでは、このマークアップ拡張機能の処理は、クラスによって定義<xref:System.Windows.Markup.TypeExtension>されます。

特定のフレームワーク実装では、値として受け<xref:System.Type>取る一部のプロパティは、型の名前 (型`Name`の文字列値) を直接受け入れることができます。 ただし、この動作を実装することは複雑なシナリオです。 例については、後述の「WPF の使用に関する注意事項」を参照してください。

属性構文は、このマークアップ拡張機能で使用される最も一般的な構文です。 `x:Type` 識別子文字列の後に設定される文字列トークンは、基になる <xref:System.Windows.Markup.TypeExtension.TypeName%2A> 拡張クラスの <xref:System.Windows.Markup.TypeExtension> 値として割り当てられます。 CLR 型に基づく .NET XAML サービスの既定の XAML スキーマ コンテキストでは、この属性の<xref:System.Reflection.MemberInfo.Name%2A>値は、目的の型の値<xref:System.Reflection.MemberInfo.Name%2A>か、既定以外の XAML 名前空間マッピングのプレフィックスが含まれています。

マークアップ`x:Type`拡張機能は、オブジェクト要素構文で使用できます。 この場合、拡張機能を正しく初期化するには、<xref:System.Windows.Markup.TypeExtension.TypeName%2A>プロパティの値を指定する必要があります。

マークアップ`x:Type`拡張機能は、詳細な属性としても使用できます。ただし、この使用は一般的ではありません。`<object property="{x:Type TypeName=typeNameValue}" .../>`

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

### <a name="default-xaml-namespace-and-type-mapping"></a>既定の XAML 名前空間と型マッピング

WPF プログラミングの既定の XAML 名前空間には、一般的な XAML シナリオに必要な XAML 型のほとんどが含まれています。したがって、XAML 型の値を参照するときにプレフィックスを回避できることがよくあります。 カスタム アセンブリから型を参照する場合、または WPF アセンブリに存在するが、既定の XAML 名前空間にマップされていない CLR 名前空間の型を参照している場合は、プレフィックスをマップする必要があります。 プレフィックス、XAML 名前空間、および CLR 名前空間のマッピングの詳細については、「 [WPF XAML の XAML 名前空間と名前空間マッピング](../../framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)」を参照してください。

### <a name="type-properties-that-support-typename-as-string"></a>文字列として型名をサポートする型プロパティ

WPF では、マークアップ拡張機能の使用を必要とせずに、型<xref:System.Type>の一部のプロパティ`x:Type`の値を指定できるようにする手法がサポートされています。 代わりに、型に名前を付け、文字列として値を指定できます。 この例は<xref:System.Windows.Controls.ControlTemplate.TargetType%2A?displayProperty=nameWithType>、<xref:System.Windows.Style.TargetType%2A?displayProperty=nameWithType>および です。 この動作のサポートは、型コンバーターまたはマークアップ拡張機能を通じて提供されません。 代わりに、 を通じて<xref:System.Windows.FrameworkElementFactory>実装される遅延動作です。

Silverlight は、同様の規則をサポートしています。 実際、現在、Silverlight は`{x:Type}`XAML 言語サポートをサポートしておらず、WPF-Silverlight XAML の移行をサポートすることを目的としたいくつかの状況以外では使用を受け付`{x:Type}`けなくなります。 したがって、文字列としての型名の動作は、値を<xref:System.Type>指定する場合、すべての Silverlight ネイティブ プロパティ評価に組み込まれています。

## <a name="xaml-2009"></a>XAML 2009

XAML 2009 では、ジェネリック型の追加サポートを提供し、`x:TypeArguments`この`x:Type`サポートを提供する機能の動作を変更します。

- `x:TypeArguments`また、汎用オブジェクトのインスタンス化に関連付けられたオブジェクト要素は、ルート以外の要素に対して使用できます。 詳細については[、「xaml](xtypearguments-directive.md)2009」セクションを参照してください。

- XAML 2009 では、マークアップでジェネリック型の制約を指定するための構文がサポートされています。 この機能は、`x:TypeArguments`によって`x:Type`、または 2 つの機能を組み合わせて使用できます。

- 読み込み用の XAML 2009 を処理する際の WPF XAML 実装は、型を<xref:System.Type>使用する特定のフレームワーク プロパティの暗黙の型変換動作にもこの機能を追加します。

WPF では、XAML 2009 の機能を使用できますが、緩い XAML (マークアップ コンパイルされていない XAML) に対してのみ使用できます。 WPF 向けにマークアップ コンパイルされた XAML、および XAML の BAML 形式は、現在、XAML 2009 のキーワードと機能をサポートしていません。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Style>
- [スタイルとテンプレート](../fundamentals/styles-templates-overview.md)
- [XAML の概要 (WPF)](../fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)
