---
title: x:FieldModifier ディレクティブ
ms.date: 03/30/2017
helpviewer_keywords:
- FieldModifier attribute in XAML [XAML Services]
- x:FieldModifier attribute [XAML Services]
- XAML [XAML Services], x:FieldModifier attribute
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
ms.openlocfilehash: 3e104b4c464d545e048f29901701c1c3dbb68229
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432780"
---
# <a name="xfieldmodifier-directive"></a>x:FieldModifier ディレクティブ
XAML コンパイル動作を変更して、名前付きオブジェクト参照のフィールド<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>が<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>既定の動作ではなくアクセスで定義されるようにします。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:FieldModifier="Public".../>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|*パブリック*|指定する文字列と<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>指定する文字列は、使用する分離コード プログラミング言語によって異なります。 「解説」を参照してください。|

## <a name="dependencies"></a>依存関係

 XAML の運用環境で`x:FieldModifier`任意の場所を使用する場合、その XAML の運用環境のルート要素は[、x: Class ディレクティブ](xclass-directive.md)を宣言する必要があります。

## <a name="remarks"></a>解説

`x:FieldModifier`クラスまたはそのメンバーの一般的なアクセス レベルを宣言する場合は、そのレベルは関係ありません。 これは、XAML の処理動作に関連する XAML の一部である特定の XAML オブジェクトが処理され、アプリケーションのオブジェクト グラフでアクセス可能なオブジェクトになる可能性があるオブジェクトになります。 既定では、このようなオブジェクトのフィールド参照はプライベートに保たれ、コントロール のコンシューマーがオブジェクト グラフを直接変更できないようにします。 代わりに、コントロール コンシューマーは、レイアウト ルート、子要素コレクション、専用のパブリック プロパティなどを取得するなど、プログラミング モデルによって有効になる標準パターンを使用してオブジェクト グラフを変更することが期待されます。

属性の`x:FieldModifier`値はプログラミング言語によって異なり、その目的は特定のフレームワークによって異なる場合があります。 使用する文字列は、各言語が実装<xref:System.CodeDom.Compiler.CodeDomProvider>する方法と、その言語が返す型コンバーターによって、 および<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>の意味を定義するかどうか、およびその言語で大文字と小文字が区別されるかどうかによって異なります。

- C# の場合、指定<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>に渡す文字列`public`は です。

- NET の場合、指定<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>に渡す文字列は`Public`です。

- C++/CLI の場合、現在 XAML のターゲットは存在しません。したがって、渡す文字列は未定義です。

(Visual Basic <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> `internal`では C#`Friend`で) 指定することもできますが<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>、動作は`NotPublic`既に既定であるため、指定は珍しいものです。

<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>XAML をコンパイルしたアセンブリの外部のコードが XAML で作成された要素にアクセスする必要がある場合は、そのコードが頻繁に発生するため、既定の動作です。 WPF セキュリティ アーキテクチャと XAML コンパイル動作を組み合わせて使用すると、パブリック アクセスを許可するように`x:FieldModifier`明示的に設定しない限り、要素インスタンスをパブリックとして格納するフィールドは宣言されません。

`x:FieldModifier`は、その名前がパブリックの後にフィールドを参照するために使用されるため[、x:Name ディレクティブ](xname-directive.md)を持つ要素にのみ関連します。

既定では、ルート要素の部分クラスはパブリックです。ただし[、x:ClassModifier ディレクティブ](xclassmodifier-directive.md)を使用して、これを非パブリックにできます。 [x:ClassModifier ディレクティブ](xclassmodifier-directive.md)は、ルート要素クラスのインスタンスのアクセス レベルにも影響します。 ルート要素`x:FieldModifier`の両方`x:Name`を配置できますが、これはルート要素のパブリック フィールド コピーのみを作成します。 [x:ClassModifier Directive](xclassmodifier-directive.md)

## <a name="see-also"></a>関連項目

- [WPF における XAML とカスタム クラス](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [WPF における分離コードと XAML](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [x:Name ディレクティブ](xname-directive.md)
- [WPF アプリケーションのビルド (WPF)](../../framework/wpf/app-development/building-a-wpf-application-wpf.md)
- [x:ClassModifier ディレクティブ](xclassmodifier-directive.md)
