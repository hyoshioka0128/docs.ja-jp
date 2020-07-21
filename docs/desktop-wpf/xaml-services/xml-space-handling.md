---
title: XAML における xml:space の処理
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:space attribute
- XAML [XAML Services], white-space processing
- xml:space attribute [XAML Services]
- white-space processing [XAML Services]
ms.assetid: 5e1814f0-5b30-43d5-8c88-dede335a89d7
ms.openlocfilehash: 886f906b6d1e3a10920dbf52e36bf76324c5a9f2
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432702"
---
# <a name="xmlspace-handling-in-xaml"></a>XAML における xml:space の処理

属性`xml:space`は、オブジェクト要素内の重要な空白の処理動作を宣言する XML 定義の属性です。 この動作は、宣言されている`xml:space`要素内に含まれるすべてのコンテンツ (内部テキスト) に関連し、子要素にも適用されます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object xml:space="preserve" />
```

 \- または

```xaml
<object xml:space="default" />
```

## <a name="remarks"></a>解説

XAML の属性`xml:space`の定義には、2 つの値を含む`xml:space`XML の W3C 仕様によって "特殊な属性" として定義されたとおりに派生します。

属性の`xml:space`デフォルト値は リテラル値`"default"`です。 value`"default"`の場合、または`xml:space`まったく指定されていない場合は、[トピック「XAML での空白処理](white-space-processing.md)」で定義されているように、重要な空白の解析の動作が既定の処理になります。

オブジェクト要素の内容内の空白を保持するには`xml:space="preserve"`、そのオブジェクト要素で指定します。

ほとんどの解釈では、属性の`xml:space`効果と属性の値は、子要素にスコープされます。

XAML での空白の処理の詳細については、「 XAML で[の空白の処理](white-space-processing.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [XAML での空白の処理](white-space-processing.md)
- [XAML の概要 (WPF)](../fundamentals/xaml.md)
