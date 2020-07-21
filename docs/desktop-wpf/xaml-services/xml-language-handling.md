---
title: XAML における xml:lang の処理
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:lang attribute
- xml:lang attribute [XAML Services]
- RFC 3066 standard [XAML Services]
- standards [XAML Services], RFC 3066
ms.assetid: 7aac0078-a1c5-41f8-b8b0-975510d9dca0
ms.openlocfilehash: b5a06adbb7cb874bc09899118f13b91fbec7a85e
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432708"
---
# <a name="xmllang-handling-in-xaml"></a>XAML における xml:lang の処理

属性`xml:lang`は、XML で要素の言語およびカルチャ情報を宣言する XML 定義の属性です。 属性の意味は XAML でも同じですが、いくつかの追加の考慮事項が適用されます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object xml:lang="rfc3066lang" />
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|*rfc3066lang*|[RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) 標準で定義されている文字列。1 つの言語、または言語と地域を表します。 後者の場合は、言語と地域が 1 つのハイフンで区切られます。 値と形式の詳細については、「 <xref:System.Windows.Markup.XmlLanguage> 」を参照してください。|

## <a name="remarks"></a>解説

属性の`xml:lang`定義[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]は、XML のワールド`xml:lang`ワイド Web コンソーシアム (W3C) によって "特殊な属性" として定義された属性から派生します。 言語およびカルチャ情報が要素によって処理される方法は、実装に応じて異なる可能性がありますが、 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] における `xml:lang` 属性の既定の処理というものは存在しません。

`xml:lang` 属性の既定値は、属性レベルで空の文字列です。

`xml:lang` 属性の効果と属性の値が、 `xml:lang` 値を処理するシステムによって解釈される場合、これらの効果と値は、通常、子要素に反映されます。

.NET XAML サービスの XAML ライターによって解釈される`xml:lang`場合、値<xref:System.Windows.Markup.XmlLanguage>は<xref:System.Globalization.CultureInfo>基になるオブジェクト表現内にオブジェクトを作成または作成できます。ただし、この動作は、指定された`xml:lang`値がそれらのクラスに対して有効な構築であるかどうかによって異なります。

フレームワークは、 `xml:lang` をプロパティに適用することによって、フレームワーク定義プロパティと XML 内の <xref:System.Windows.Markup.XmlLangPropertyAttribute> の意味を関連付けることができます。

## <a name="wpf-usage-nodes"></a>WPF の使用上の注意

要素が <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement>の派生クラスの場合は、 <xref:System.Windows.FrameworkElement.Language%2A> 属性の代わりに、同等の `xml:lang` 依存関係プロパティを使用できます。 別途設定されない限り、 <xref:System.Windows.FrameworkElement.Language%2A> プロパティの値は既定で "en-US" となります。このプロパティの値は、このプロパティを通して、または `xml:lang` 属性を処理することによって設定されます。

## <a name="see-also"></a>関連項目

- [WPF のグローバリゼーション](../../framework/wpf/advanced/globalization-for-wpf.md)
