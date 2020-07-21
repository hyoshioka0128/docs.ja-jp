---
title: '{}エスケープ シーケンス - マークアップ拡張機能'
ms.date: 03/30/2017
f1_keywords:
- '{}'
helpviewer_keywords:
- XAML [XAML Services], quotation mark (")
- '{} escape sequence [XAML Services]'
- XAML [XAML Services], {} escape sequence
- XAML [XAML Services], escape sequence
- quotation mark (") [XAML Services]
- escape sequence [XAML Services]
ms.assetid: 3ce3e2ad-a868-43f9-9c98-b29561cb146e
ms.openlocfilehash: f84243994557d76fa52d72b060a1ba35460e98b0
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432966"
---
# <a name="-escape-sequence--markup-extension"></a>{}エスケープ シーケンス/マークアップ拡張機能

属性値の XAML エスケープ シーケンスを提供します。 エスケープ シーケンスを使用すると、属性内の後続の値をリテラルとして解釈できます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object property="{} literalValue" .../>
```

## <a name="xaml-property-element-usage"></a>XAML プロパティ要素の使用

```xaml
<object>
  <object.property>
    {} literalValue
  </object.property>
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|*リテラル値*|エスケープ シーケンスの後に続くリテラル文字列。 通常、この文字列には、左または右かっこ ({または }) が含まれています。|

## <a name="remarks"></a>解説

XAML では、{}左中かっこ ({) をリテラル文字として使用できるように、エスケープ シーケンス ( ) が使用されます。

XAML リーダーは、通常、マークアップ拡張機能のエントリ ポイントを示すために、左中かっこ ({) を使用しますが、最初に次の文字をチェックして、右中かっこ (}) であるかどうかを判断します。 2 つの中かっこ ({}) が隣接している場合にのみ、エスケープ シーケンスと見なされます。

エスケープ シーケンスが検出された場合、XAML リーダーは文字列の残りの部分を文字列として処理する必要があります。 ただし、エスケープ シーケンスが型コンバーターを持つメンバーに適用される場合、文字列は XAML ライターによって解釈されるときに型変換を受ける可能性があります。

エスケープ シーケンスはマークアップ拡張機能ではなく、クラスによってバックされるわけではありません。 ただし、これは XAML リーダー (カスタム XAML リーダーを含む) が尊重すべき規則です。

引用符 (") は、この方法でエスケープ シーケンスとして使用することはできません。 非コンテンツ プロパティのプロパティ値として引用符を設定する必要がある場合は、プロパティ要素構文を使用し、引用符をプロパティ要素内の文字列として配置するか、XML 文字エンティティを使用します。 コンテンツ プロパティの場合、引用符はコンテンツ全体にすることができます。

XAML マークアップ拡張機能{}が出現する可能性がある場所に名前空間修飾子を含める必要がある XML 型を指定する場合、エスケープ シーケンス ( ) が頻繁に必要です。 この場所には、XAML 属性値の開始と、等号 (=) の直後のマークアップ拡張機能が含まれます。 XAML 属性値の先頭に表示される XML 名前空間のエスケープ シーケンスを次の例に示します。

[!code-xaml[XLINQExample#StackPanelResources](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]

## <a name="see-also"></a>関連項目

- [XAML の型コンバーターおよびマークアップ拡張機能](type-converters-and-markup-extensions.md)
- [XML 文字エンティティと XAML](xml-character-entities.md)
