---
title: x:Reference のマークアップ拡張機能
ms.date: 03/30/2017
helpviewer_keywords:
- x:Reference markup extension [XAML Services]
- XAML [XAML Services], x:Reference Markup Extension
- Reference markup extension [XAML Services]
ms.assetid: 2982e68b-d26b-4aa3-826a-34c57a9c5199
ms.openlocfilehash: f06e259893111a436e5afe2df754c3edee326d54
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432654"
---
# <a name="xreference-markup-extension"></a>x:Reference のマークアップ拡張機能

XAML マークアップ内の他の場所で宣言されているインスタンスを参照します。 参照は要素の`x:Name`を参照します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object property="{x:Reference instancexName}" .../>
```

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xaml
<object>
  <object.property>
    <x:Reference Name="instancexName"/>
  </object.property>
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`instancexName`|参照`x:Name`先インスタンスの<xref:System.Windows.Markup.RuntimeNamePropertyAttribute>値 (または -識別プロパティの値)。|

## <a name="remarks"></a>解説

`x:Reference`WPF などの特定のフレームワークで実装された要素参照の概念に対する XAML 言語レベルのサポートを提供します。

## <a name="xreference-and-wpf"></a>x:リファレンスとWPF

WPF および XAML 2006 では、要素参照はバインディングの<xref:System.Windows.Data.Binding.ElementName%2A>フレームワーク レベルの機能によって解決されます。 ほとんどの WPF アプリケーションおよびシナリオでは<xref:System.Windows.Data.Binding.ElementName%2A>、バインディングを使用する必要があります。 この一般的なガイダンスの例外として、データ バインディングを実用的でなくて、マークアップのコンパイルが関係しないデータ コンテキストやその他のスコープの考慮事項がある場合が含まれる場合があります。

`x:Reference`は、XAML 2009 で定義された構造です。 WPF では XAML 2009 の機能を使用できますが、WPF マークアップ コンパイルされていない XAML に限定されます。 マークアップ コンパイルされた XAML、および XAML の BAML 形式は、現在、XAML 2009 言語のキーワードと機能をサポートしていません。
