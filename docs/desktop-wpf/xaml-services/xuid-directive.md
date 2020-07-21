---
title: x:Uid ディレクティブ
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], localizable content attribute
- XAML [XAML Services], x:Uid attribute
- x:Uid attribute [XAML Services]
- Uid attribute [XAML Services]
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
ms.openlocfilehash: b5b480016d2183268422dea861510c6a169ac27b
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432618"
---
# <a name="xuid-directive"></a>x:Uid ディレクティブ

マークアップ要素の一意の識別子を提供します。 多くのシナリオでは、この一意の識別子は、XAML のローカリゼーション プロセスとツールで使用されます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:Uid="identifier"... />
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`identifier`|手動で作成された文字列、またはコンシューマーによって解釈されるときにファイル内で一意である必要がある自動生成`x:Uid`された文字列。|

## <a name="remarks"></a>解説

[MS-XAML]では、`x:Uid`ディレクティブとして定義されます。 詳細については、「 [ \[MS-XAML\]セクション 5.3.6](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))」を参照してください。

`x:Uid`は、記載`x:Name`されている XAML ローカリゼーション シナリオと、ローカライズに使用される識別子が のプログラミング モデルへの依存性を持たないため`x:Name`、両方から離散的です。 また、XAML`x:Name`名前スコープによって制御されます。ただし、`x:Uid`一意性の適用に関する XAML 言語定義の概念によって制御されるわけではありません。 広い意味での XAML プロセッサ (ローカリゼーション プロセスの一部ではないプロセッサ) は、値`x:Uid`の一意性を強制することは期待されていません。 その責任は概念的に値の創始者にあります。 単一の XAML`x:Uid`ソース内の値の一意性の期待は、専用のグローバリゼーション プロセスやツールなどの値のコンシューマーにとって妥当です。 一般的な一意性モデル`x:Uid`は、XAML を表す XML エンコード ファイル内で値が一意であるというものです。

特定の XAML スキーマに関する重要な知識を持`x:Uid`つツールは、マークアップでテキスト文字列値が検出されるすべての場合ではなく、真のローカライズ可能な文字列にのみ適用するように選択できます。

フレームワークは、定義する型に属性`x:Uid`<xref:System.Windows.Markup.UidPropertyAttribute>を適用することで、オブジェクト モデル内の特定のプロパティをエイリアスとして指定できます。 フレームワークが特定のプロパティを指定する場合、同じオブジェクトに対`x:Uid`してエイリアス化されたメンバーの両方を指定することは無効です。 エイリアスを`x:Uid`付けたメンバーの両方を指定すると、.NET XAML サービス<xref:System.Xaml.XamlDuplicateMemberException>API は通常、このケースをスローします。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

WPF ローカリゼーション`x:Uid`プロセスおよび BAML 形式の XAML での役割の詳細については[、「WPF のグローバリゼーション」または「WPF のグローバリゼーション](../../framework/wpf/advanced/globalization-for-wpf.md)」を参照してください。<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>
- <xref:Microsoft.Build.Tasks.Windows.UidManager>
- [WPF のグローバリゼーション](../../framework/wpf/advanced/globalization-for-wpf.md)
