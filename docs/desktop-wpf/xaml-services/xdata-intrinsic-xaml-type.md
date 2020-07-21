---
title: x:XData 組み込み XAML 型
ms.date: 03/30/2017
f1_keywords:
- x:XData
- XData
- xXData
helpviewer_keywords:
- XAML [XAML Services], x:XData directive element
- XData in XAML [XAML Services]
- x:XData XAML directive element [XAML Services]
ms.assetid: 7ce209c2-621b-4977-b643-565f7e663534
ms.openlocfilehash: b7f0954158988db107feb4a6c51ba81d5db11dcb
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432792"
---
# <a name="xxdata-intrinsic-xaml-type"></a>x:XData 組み込み XAML 型
XAML の運用環境内で XML データ アイランドを配置できるようにします。 内部の`x:XData`XML 要素は、動作する既定の XAML 名前空間またはその他の XAML 名前空間の一部であるかのように XAML プロセッサによって扱われるべきではありません。 `x:XData`任意の整形式 XML を含めることができます。

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xaml
<x:XData>
  <elementDataRoot>
    [elementData]
  </elementDataRoot>
</x:XData>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`elementDataRoot`|囲まれたデータ アイランドの単一のルート要素。 ほとんどの最終的なコンシューマーでは、ルートが 1 つもたない XML は無効と見なされます。 特に、WPF の XML データ`x:XData`ソースとして、またはデータ バインディングに XML ソースを使用するその他の多くのテクノロジを目的とする場合は、単一のルートが必要です。|
|`[elementData]`|省略可能。 XML データを表す XML。 要素データとして任意の数の要素を含めることができ、入れ子になった要素は他の要素に含めることができます。ただし、XML の一般的な規則が適用されます。|

## <a name="remarks"></a>解説

オブジェクト内の`x:XData`XML 要素は、データ内の XMLDOM を含む名前空間とプレフィックスをすべて再宣言できます。

XML データおよび`x:XData`組み込み XAML 型へのプログラムによるアクセスは、クラスを<xref:System.Windows.Markup.XData>通じて .NET XAML サービスで可能です。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

オブジェクト`x:XData`は主に<xref:System.Windows.Data.XmlDataProvider>、 の子オブジェクトとして使用されるか、または<xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=nameWithType>プロパティの子オブジェクトとして使用されます (XAML では、通常はプロパティ要素構文で表されます)。

通常、データ アイランド内の基本 XML 名前空間を新しい既定の XML 名前空間 (空の文字列に設定) に再定義する必要があります。 データの参照とバインドに使用される式<xref:System.Windows.Data.Binding.XPath%2A>はプレフィックスを含めることを避けることができるので、これは単純なデータ アイランドにとって最も簡単です。 より複雑なデータ アイランドでは、データに対して複数のプレフィックスを定義し、ルートにある XML 名前空間に特定のプレフィックスを使用する場合があります。 この場合、すべての<xref:System.Windows.Data.Binding.XPath%2A>式参照には、適切な名前空間マップのプレフィックスを含める必要があります。 詳細については、「[データ バインディングの概要](../data/data-binding-overview.md)」を参照してください。

技術的には`x:XData`、 型<xref:System.Xml.Serialization.IXmlSerializable>の任意のプロパティの内容として使用できます。 しかし、<xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=nameWithType>唯一の顕著な実装です。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.XmlDataProvider>
- [データ バインディングの概要](../data/data-binding-overview.md)
- [バインドのマークアップ拡張機能](../../framework/wpf/advanced/binding-markup-extension.md)
