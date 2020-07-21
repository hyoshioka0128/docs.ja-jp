---
title: x:Null のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- NullExtension
- x:NullExtension
- x:Null
- "Null"
- xNull
helpviewer_keywords:
- Null markup extension in XAML [XAML Services]
- x:Null markup extension [XAML Services]
- XAML [XAML Services], x:Null markup extension
ms.assetid: 2e3ccc21-4996-481d-91b5-3910d8b3bfa3
ms.openlocfilehash: b83e893f951c15eca69fbb6b002369dd723ca469
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432696"
---
# <a name="xnull-markup-extension"></a>x:Null のマークアップ拡張機能

XAML`null`メンバーの値として指定します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object property="{x:Null}" .../>
```

## <a name="remarks"></a>解説

C# および C++ の null 参照のキーワードは null です。 Null 参照の Visual Basic キーワード`Nothing`は で、XAML`{x:Null}`に関連付ける分離コード言語に関係なく、常に XAML の使用方法として使用します。

`x:Null`マークアップ拡張機能には、設定可能なプロパティがありません。

NULL の使用は、多くの場合、CLR<xref:System.Nullable%601>値の XAML メンバーの公開に関連付けられます。

マークアップ`x:Null`拡張機能は、すべての XAML マークアップ拡張機能と同様に、リテラル`{,}`やイベント ハンドラー参照以外の属性値の処理をエスケープするために中かっこ ( ) を使用します。 属性構文は、このマークアップ拡張機能で最もよく使用される構文です。 オブジェクト要素構文`<x:Null />`は技術的には可能ですが、`x:Null`マークアップ拡張機能には位置指定パラメータや構築引数がないため、ほとんど使用されません。

マークアップ拡張機能の詳細については、「[マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)」を参照してください。

NET XAML サービスでは、このマークアップ拡張機能の処理は、クラスによって定義<xref:System.Windows.Markup.NullExtension>されます。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

参照型`null`の依存関係プロパティの初期の未設定値である必要はありません。 初期既定値は、依存関係プロパティごとに異なる場合があり、プロパティ固有のメタデータに基づいて設定できます。 多くの依存関係プロパティは、`null`検証コールバックの実装により、マークアップまたはコードを使用して値として受け入れれません。 依存関係プロパティの詳細については、「[依存関係プロパティの概要](../../framework/wpf/advanced/dependency-properties-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.DependencyProperty.UnsetValue>
- [XAML の概要 (WPF)](../fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)
