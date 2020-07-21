---
title: x:Array のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- x:Array
- xArray
helpviewer_keywords:
- x:Array [XAML Services]
- XAML [XAML Services], x:Array markup extension
ms.assetid: c5358e14-d24c-44c7-b5eb-6062a4fd981c
ms.openlocfilehash: b332c43d7f9ffe2117c9afe1ed625c3e3c869813
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "81433284"
---
# <a name="xarray-markup-extension"></a>x:Array のマークアップ拡張機能

マークアップ拡張機能を使用して、XAML のオブジェクトの配列に対する一般的なサポートを提供します。 これは [MS-XAML] の`x:ArrayExtension`XAML 型に対応します。

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xaml
<x:Array Type="typeName">
  arrayContents
</x:Array>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`typeName`|含`x:Array`める型の名前。 `typeName`XAML 型定義を含む XAML 名前空間のプレフィックスが付くこともあります (多くの場合、|
|`arrayContents`|組み込み`ArrayExtension.Items`プロパティに割り当てられている項目のコンテンツ。 通常、これらの項目は、開始タグと終了タグに含まれる`x:Array`1 つ以上のオブジェクト要素として指定されます。 ここで指定したオブジェクトは、 で`typeName`指定された XAML 型に割り当て可能であると想定されます。|

## <a name="remarks"></a>解説

`Type`は、すべての`x:Array`オブジェクト要素に必須の属性です。 `Type`パラメーター値は`x:Type`マークアップ拡張機能を使用する必要はありません。型の短い名前は XAML 型で、文字列として指定できます。

NET XAML サービスの実装では、入力 XAML 型と作成された配列<xref:System.Type>の出力 CLR の関係は、マークアップ拡張機能のサービス コンテキストによって影響を受けます。 出力<xref:System.Type>は、XAML<xref:System.Xaml.XamlType.UnderlyingType%2A>スキーマ コンテキストとコンテキストが提供するサービスに<xref:System.Xaml.XamlType>基づいて必要な検索を行<xref:System.Windows.Markup.IXamlTypeResolver>った後の入力 XAML 型です。

処理されると、配列の内容は組み込`ArrayExtension.Items`みプロパティに割り当てられます。 実装では<xref:System.Windows.Markup.ArrayExtension>、これは<xref:System.Windows.Markup.ArrayExtension.Items%2A?displayProperty=nameWithType>で表されます。

NET XAML サービスの実装では、このマークアップ拡張機能の処理は、クラスによって<xref:System.Windows.Markup.ArrayExtension>定義されます。 <xref:System.Windows.Markup.ArrayExtension>はシールされておらず、カスタム配列型のマークアップ拡張機能の実装の基礎として使用できます。

`x:Array`XAML の一般的な言語拡張機能を目的としています。 ただし`x:Array`、構造化されたプロパティ コンテンツとして XAML でサポートされているコレクションを受け取る特定のプロパティの XAML 値を指定する場合にも役立ちます。 たとえば、<xref:System.Collections.IEnumerable>`x:Array`プロパティの内容を使用して指定できます。

`x:Array` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 `x:Array`は、代替の属性値の処理を提供する代わりに、その内部テキスト`x:Array`コンテンツの代替処理を提供するため、そのルールの部分的な例外です。 この動作により、既存のコンテンツ モデルでサポートされていない型を配列にグループ化し、名前付き配列にアクセスして分離コード内で参照できます。メソッドを呼<xref:System.Array>び出して、個々の配列項目を取得できます。

XAML のすべてのマークアップ拡張機能では、中かっこ{,}`)`(属性構文で、XAML プロセッサがマークアップ拡張機能が属性値を処理する必要があることを認識する規則) を使用します。 マークアップ拡張機能全般の詳細については、「 XAML の[型コンバーターとマークアップ拡張機能](type-converters-and-markup-extensions.md)」を参照してください。

XAML 2009`x:Array`では、マークアップ拡張機能ではなく言語プリミティブとして定義されます。 詳細については、「[共通言語 XAML 言語プリミティブの組み込み型](types-for-primitives.md)」を参照してください。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

通常、値を設定するオブジェクト要素`x:Array`は[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]XAML 名前空間に存在する要素ではなく、既定以外の XAML 名前空間へのプレフィックス マッピングを必要とします。

たとえば、次の例は`sys`、2 つの文字列の単純な配列で、プレフィックス`x`(および) が配列のレベルで定義されています。

```xaml
<x:Array Type="sys:String"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:sys="clr-namespace:System;assembly=mscorlib">
  <sys:String>Hello</sys:String>
  <sys:String>World</sys:String>
</x:Array>
```

配列要素として使用されるカスタム型の場合、クラスは XAML でオブジェクト要素としてインスタンス化するための要件もサポートする必要があります。 詳細については、「 [WPF の XAML とカスタム クラス](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)
- [WPF から System.Xaml に移行した型](../../framework/wpf/advanced/types-migrated-from-wpf-to-system.md)
