---
title: XAML のジェネリック
ms.date: 03/30/2017
helpviewer_keywords:
- generics [XAML Services]
ms.assetid: 835bfed7-585c-4216-ae67-b674edab8b92
ms.openlocfilehash: 9354f74b978652c36df28a91a6b9db5cfff4bb1e
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432960"
---
# <a name="generics-in-xaml"></a>XAML のジェネリック

に実装されている .NET XAML<xref:System.Xaml?displayProperty=fullName>サービスは、ジェネリック CLR 型の使用をサポートします。 このサポートには、ジェネリックの制約を型引数として指定し、ジェネリック コレクションのケースに対して`Add`適切なメソッドを呼び出して制約を適用する機能が含まれます。 このトピックでは、XAML でジェネリック型を使用および参照する方法について説明します。

## <a name="xtypearguments"></a>x:型引数

`x:TypeArguments`は、XAML 言語で定義されたディレクティブです。 ジェネリック型によってサポートされる XAML 型のメンバーとして使用する場合、`x:TypeArguments`ジェネリックの制約型引数をバッキング コンストラクターに渡します。 の .NET XAML サービスの`x:TypeArguments`使用に関連する参照構文については[、「x:TypeArguments ディレクティブ](xtypearguments-directive.md)」を参照してください。

文字列`x:TypeArguments`を受け取り、型コンバーターのバッキングがあるため、通常は XAML で属性として宣言されます。

XAML ノード ストリームでは、 によって`x:TypeArguments`宣言された情報は、<xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=nameWithType>ノード`StartObject`ストリーム内の位置から取得できます。 の戻り値<xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=nameWithType>は、値の<xref:System.Xaml.XamlType>リストです。 XAML 型がジェネリック型を表すかどうかを確認するには、 を<xref:System.Xaml.XamlType.IsGeneric%2A?displayProperty=nameWithType>呼び出します。

## <a name="rules-and-syntax-conventions-for-generics-in-xaml"></a>XAML のジェネリックの規則と構文の規則

XAML では、ジェネリック型は常に制約付きジェネリックとして表す必要があります。 制約のないジェネリックは、XAML 型システムまたは XAML ノード ストリームには存在しません。 ジェネリックは、XAML 属性構文内で参照できます。 `x:TypeArguments` `x:Type` ジェネリックの参照は、.NET <xref:System.Xaml.Schema.XamlTypeTypeConverter> XAML サービスで定義されたクラスを通じてサポートされます。

ジェネリックの型と制約に山<xref:System.Xaml.Schema.XamlTypeTypeConverter>かっこを使用し、代わりに制約コンテナーのかっこを置き換える、一般的な MSIL /CLR 構文規則を変更することによって有効にされた XAML 属性構文フォーム。 例については、「 [x:TypeArguments ディレクティブ](xtypearguments-directive.md)」を参照してください。

## <a name="generics-and-xaml-2009-features"></a>ジェネリックと XAML 2009 の機能

共通言語プリミティブの XAML 型を取得するために CLR 基本型をマッピングする代わりに XAML 2009 を使用する場合は、 の`x:TypeArguments`情報項目として XAML [2009 の組み込み型を](types-for-primitives.md)使用できます。 たとえば、次のように宣言できます (プレフィックス マッピングは表示されませんが`x`、XAML 2009 の XAML 言語 XAML 名前空間です)。

```xaml
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>
```

## <a name="generics-support-in-wpf"></a>WPF でのジェネリックサポート

特に WPF を対象とする XAML 2006 の使用法では[、x:](xclass-directive.md) `x:TypeArguments`Class は と同じ要素に対しても指定する必要があり、その要素は XAML ドキュメントのルート要素である必要があります。 ルート要素は、少なくとも 1 つの型引数を持つジェネリック型にマップする必要があります。 たとえば <xref:System.Windows.Navigation.PageFunction%601> です。

ジェネリックの使用法をサポートする場合の回避策としては、ジェネリック型を返すことができるカスタム マークアップ拡張機能の定義や、ジェネリック型から派生するが、独自のクラス定義でジェネリック制約をフラット化するラップ クラス定義の提供などがあります。

WPF では、XAML 2009 機能を`x:TypeArguments`と共に使用できますが、緩い XAML (マークアップ コンパイルされていない XAML) に対してのみ使用できます。 WPF 向けにマークアップ コンパイルされた XAML、および XAML の BAML 形式は、現在、XAML 2009 のキーワードと機能をサポートしていません。

.NET Framework 3.5 の Windows ワークフロー基盤のカスタム ワークフローでは、一般的な XAML の使用法はサポートされていません。

## <a name="see-also"></a>関連項目

- [x:TypeArguments ディレクティブ](xtypearguments-directive.md)
- [x:Class ディレクティブ](xclass-directive.md)
- [共通の XAML 言語プリミティブの組み込み型](types-for-primitives.md)
