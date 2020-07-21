---
title: x:ClassModifier ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- xClassModifier
- x:ClassModifier
- ClassModifier
helpviewer_keywords:
- XAML [XAML Services], x:ClassModifier attribute
- x:ClassModifier attribute [XAML Services]
- ClassModifier attribute in XAML [XAML Services]
ms.assetid: ef30ab78-d334-4668-917d-c9f66c3b6aea
ms.openlocfilehash: 436204774c2d59b43a77865c666aed702f7681db
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "81433272"
---
# <a name="xclassmodifier-directive"></a>x:ClassModifier ディレクティブ
XAML コンパイル動作を変更`x:Class`します。 具体的には、アクセス レベル`class`(既定)`Public`を持つ部分を作成する`x:Class`代わりに、提供`NotPublic`されるアクセス レベルを使用して作成されます。 この動作は、生成されたアセンブリ内のクラスのアクセス レベルに影響します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:Class="namespace.classname" x:ClassModifier="NotPublic">
   ...
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|*公開されていない*|指定する文字列と<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>指定する文字列は、使用する分離コード プログラミング言語によって異なります。 「解説」を参照してください。|

## <a name="dependencies"></a>依存関係

[x:Class](xclass-directive.md)も同じ要素に指定する必要があり、その要素はページのルート要素である必要があります。 詳細については、 [ \[MS-XAML\]セクション 4.3.1.8](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。

## <a name="remarks"></a>解説

.NET `x:ClassModifier` XAML サービスの使用法の値は、プログラミング言語によって異なります。 使用する文字列は、各言語が実装<xref:System.CodeDom.Compiler.CodeDomProvider>する方法と、その言語が返す型コンバーターによって、 および<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>の意味を定義するかどうか、およびその言語で大文字と小文字が区別されるかどうかによって異なります。

- C# の場合、指定<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>に渡す文字列`internal`は です。

- NET の場合、指定<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>に渡す文字列は`Friend`です。

- C++/CLI の場合、XAML のコンパイルをサポートするターゲットは存在しません。したがって、渡す値は指定されません。

(C#<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>では`public`Visual `Public` Basic で) 指定することもできます。ただし、指定は<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>既にデフォルトの動作<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>であるため、あまり行われません。

C# など`private`、同等のユーザー コード アクセス レベル制限を持つ他の値は`x:ClassModifier`、入れ子になったクラス参照は XAML ではサポートされていないため、<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>修飾子の効果は同じであるため、関連しません。

## <a name="security-notes"></a>セキュリティに関するメモ

で宣言されたアクセス レベル`x:ClassModifier`は、特定のフレームワークとその機能による解釈の対象となります。 WPF には、pack URI 参照を`x:ClassModifier`通`internal`じて WPF リソースからクラスが参照されている場合に、 の型を読み込んでインスタンス化する機能が含まれています。 このケースの結果として、他のフレームワークによって実装されたような潜在的に他の人は、すべての可能な`x:ClassModifier`インスタンス化の試みをブロックするために排他的に依存しないでください。

## <a name="see-also"></a>関連項目

- [x:Class ディレクティブ](xclass-directive.md)
- [WPF における分離コードと XAML](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [x:FieldModifier ディレクティブ](xfieldmodifier-directive.md)
- [セキュリティ (WPF)](../../framework/wpf/security-wpf.md)
- [WPF から System.Xaml に移行した型](../../framework/wpf/advanced/types-migrated-from-wpf-to-system.md)
