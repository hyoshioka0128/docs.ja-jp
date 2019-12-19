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
ms.openlocfilehash: a24277a4d5fbc4870157b6c8ba00ba71ba61e656
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837234"
---
# <a name="xclassmodifier-directive"></a>x:ClassModifier ディレクティブ
`x:Class` が指定されている場合に XAML のコンパイル動作を変更します。 具体的には、`Public` アクセスレベル (既定値) を持つ部分 `class` を作成するのではなく、指定された `x:Class` が `NotPublic` アクセスレベルで作成されます。 この動作は、生成されたアセンブリのクラスのアクセスレベルに影響します。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用  
  
```xaml  
<object x:Class="namespace.classname" x:ClassModifier="NotPublic">  
   ...  
</object>  
```  
  
## <a name="xaml-values"></a>XAML の値  
  
|||  
|-|-|  
|*NotPublic*|<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> と <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> を指定するために渡す文字列は、使用する分離コードプログラミング言語によって異なります。 「解説」を参照してください。|  
  
## <a name="dependencies"></a>の依存関係  
 [x:Class](x-class-directive.md)も同じ要素に指定する必要があり、その要素はページのルート要素である必要があります。 詳細については、「 [\[\]」セクション 4.3.1.8](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。  
  
## <a name="remarks"></a>Remarks  
 XAML サービスの使用 .NET Framework の `x:ClassModifier` の値は、プログラミング言語によって異なります。 使用する文字列は、各言語が <xref:System.CodeDom.Compiler.CodeDomProvider> を実装する方法、および <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> と <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>の意味を定義するために返す型コンバーターと、その言語で大文字と小文字を区別するかどうかによって異なります。  
  
- のC#場合、<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> を指定するために渡す文字列は `internal`です。  
  
- Microsoft Visual Basic .NET の場合、<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> を指定するために渡す文字列は `Friend`です。  
  
- /Cli C++では、XAML のコンパイルをサポートするターゲットは存在しません。したがって、渡す値は指定されていません。  
  
 <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> を指定することもできますC#(`public` では、`Public` Visual Basic)。ただし、<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> は既に既定の動作であるため、<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> の指定はほとんど行われません。  
  
 入れ子になったクラス参照は XAML でサポートされていないC#ため、<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> 修飾子は同じ効果を持つため、ユーザーコードのアクセスレベル制限が同等の他の値 (`private` など) は `x:ClassModifier` には関係ありません。  
  
## <a name="security-notes"></a>セキュリティに関するメモ  
 `x:ClassModifier` で宣言したアクセスレベルは、特定のフレームワークとその機能によって解釈されることもあります。 WPF には、`x:ClassModifier` が `internal`されている型を読み込んでインスタンス化する機能が含まれています。これは、そのクラスが、パッケージ URI 参照を通じて WPF リソースから参照されている場合です。 このケースの結果として、他のフレームワークによって実装されている可能性がある他の場合は、`x:ClassModifier` に排他的に依存して、可能性のあるすべてのインスタンス化試行をブロックすることは避けてください。  
  
## <a name="see-also"></a>参照

- [x:Class ディレクティブ](x-class-directive.md)
- [WPF における分離コードと XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [x:FieldModifier ディレクティブ](x-fieldmodifier-directive.md)
- [セキュリティ (WPF)](../wpf/security-wpf.md)
- [WPF から System.Xaml に移行した型](types-migrated-from-wpf-to-system-xaml.md)
