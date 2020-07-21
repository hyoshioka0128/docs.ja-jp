---
title: XAML のコレクションおよびコレクション型
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 2ec58026c605df31489c8aab4c4cc714dab11474
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "81432582"
---
# <a name="collections-and-collection-types-for-xaml"></a>XAML のコレクションとコレクション型

この資料では、コレクションをサポートする型のプロパティを定義する方法、およびコレクション項目を親オブジェクト要素またはプロパティ要素の要素子としてインスタンス化するための XAML 構文をサポートする方法について説明します。

## <a name="xaml-collection-concepts"></a>XAML コレクションの概念

概念的には、XAML オブジェクト要素または XAML プロパティ要素のスコープ内に複数の子項目がある XAML 内のリレーションシップは、コレクションとして実装する必要があります。 このコレクションは、そのリレーションシップの親である XAML 型の特定の XAML プロパティに関連付ける必要があります。 XAML プロセッサは、マークアップ内の各項目を、バッキング コレクション プロパティの新しく追加された項目に割り当てる必要があるため、プロパティはコレクションである必要があります。

XAML 言語レベルでは、コレクション サポートの正確な要件が完全には定義されていません。 コレクションはリストまたはディクショナリ (両方は使用できません) の概念は XAML 言語レベルで定義されますが、どのバッキング型がリストまたはディクショナリを表すかは XAML 言語では定義されていません。

.NET XAML サービスでは、XAML コレクション サポートの概念は、.NET バッキングの種類の観点から明確に定義されています。 具体的には、コレクションの XAML サポートは、一般的な .NET プログラミングでリストとディクショナリに使用されるいくつかの .NET 概念と API に基づいています。

1. インターフェイス<xref:System.Collections.IList>はリスト コレクションを示します。

2. インターフェイス<xref:System.Collections.IDictionary>は、ディクショナリ コレクションを示します。

3. <xref:System.Array>は配列を表し、配列は<xref:System.Collections.IList>メソッドをサポートします。

これらの各コレクション概念では、.NET XAML サービス XAML プロセッサは`Add`、コレクション プロパティの型の特定のインスタンスでメソッドを呼び出すことを想定しています。 また、シリアル化のシナリオでは、XAML プロセッサは、リスト、ディクショナリ、または配列内の各項目に対して、各コレクションの特定の概念である "Items" に基づいて、個別の XAML 型のインスタンスを生成します。 これらの項目は次<xref:System.Collections.IList.Item%2A?displayProperty=nameWithType>のとおりです。<xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>;の明示的<xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType>な<xref:System.Array>.

## <a name="generic-collections"></a>ジェネリック コレクション

ジェネリック コレクションは、一般的な .NET プログラミングに役立つほか、XAML コレクション プロパティにも使用できます。 ただし、ジェネリック インターフェイス<xref:System.Collections.Generic.IList%601>と<xref:System.Collections.Generic.IDictionary%602>は、非ジェネリック<xref:System.Collections.IList>または<xref:System.Collections.IDictionary>に相当するものとして.NET XAML サービス XAML プロセッサによって識別されません。 ジェネリック コレクション プロパティ型の推奨される方法は、インターフェイスを実装するのではなく、クラス<xref:System.Collections.Generic.List%601>または<xref:System.Collections.Generic.Dictionary%602>から派生することです。 これらのクラスは、非ジェネリック インターフェイスを実装するため、基本実装で XAML コレクションの期待されるサポートが含まれます。

## <a name="read-only-collections-and-initialization-logic"></a>読み取り専用コレクションと初期化ロジック

.NET プログラミングでは、コレクションの値を保持するプロパティを読み取り専用コレクションとして格納する場合、一般的なデザイン パターンです。 このパターンにより、コレクション プロパティを所有するインスタンスが、コレクションに対する処理をより適切に制御できます。 具体的には、このパターンは、プロパティを設定することによって、既存のコレクション全体を誤って置換することを防ぎます。 このパターンでは、コレクション型や関連するコレクション インターフェイス (またはそのいずれか) でサポートされているメソッドまたはプロパティを呼び出すことによって、呼び出し元による<xref:System.Collections.IList>コレクションへのアクセスを行う必要があります。

このパターンを使用すると、読み取り専用のコレクション プロパティを公開するクラスは、最初にそのプロパティを初期化して空のコレクションを保持する必要があります。 通常、初期化はクラスの構築動作の一部として実行されます。 XAML で役立つには、XAML は、通常、プロパティ (コレクション プロパティなど) を処理する前にパラメーターなしのコンストラクターを呼び出すため、このようなロジックは常にパラメーターなしのコンストラクターによって参照される必要があります。

## <a name="xaml-type-system-support-and-collections"></a>XAML 型システム サポートとコレクション

XAML の解析とコレクション プロパティの設定またはシリアル化の基本的な仕組み以外にも、.NET XAML Services に実装されている XAML 型システムには、XAML のコレクションに関連するいくつかのデザイン機能が含まれています。

1. <xref:System.Xaml.XamlType.IsCollection%2A>XAML コレクションサポートを提供する型によって XAML 型がサポートされている場合は true を返します。

2. <xref:System.Xaml.XamlType.IsDictionary%2A>XAML<xref:System.Xaml.XamlType.IsArray%2A>型がサポートするコレクション モードをさらに識別できます。 NET XAML サービスと XAML 型システムに基づくカスタム XAML プロセッサの場合、既存<xref:System.Xaml.XamlWriter>の実装に基づいてはいませんが、コレクション処理のために呼び出すメソッドを知るためには、どのコレクション モードが使用されているかを知る必要があります。

3. 前の各プロパティ値は、XAML 型の<xref:System.Xaml.XamlType.LookupCollectionKind%2A>オーバーライドの影響を受ける可能性があります。
