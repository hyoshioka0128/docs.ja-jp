---
title: ジェネリック コレクションを使用する状況
ms.date: 04/30/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- collections [.NET Framework], generic
- generic collections [.NET Framework]
ms.assetid: e7b868b1-11fe-4ac5-bed3-de68aca47739
ms.openlocfilehash: c59a125a8df95e3c4fe6e1839956d800bd6ee910
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290384"
---
# <a name="when-to-use-generic-collections"></a>ジェネリック コレクションを使用する状況

ジェネリック コレクションでは、基本コレクション型から派生して型固有のメンバーを実装することなく、タイプ セーフの利点を即座に得ることができます。 また、ジェネリックでは要素をボックス化する必要がないため、コレクションの要素が値型である場合、一般的に、ジェネリック コレクション型は、対応する非ジェネリック コレクション型 (および、非ジェネリックの基本コレクション型から派生した型) よりもパフォーマンスに優れています。

.NET Standard 1.0 以降を対象にしたプログラムで、複数のスレッドで同時に項目をコレクションに追加またはコレクションから削除する可能性がある場合は、<xref:System.Collections.Concurrent> 名前空間のジェネリック コレクション クラスを使用します。 また、不変にする必要がある場合は、<xref:System.Collections.Immutable> 名前空間のジェネリック コレクション クラスを検討してください。

次のジェネリック型は、既存のコレクション型に対応しています。

- <xref:System.Collections.Generic.List%601> は、 <xref:System.Collections.ArrayList>に対応するジェネリック クラスです。

- <xref:System.Collections.Generic.Dictionary%602> および <xref:System.Collections.Concurrent.ConcurrentDictionary%602> は、 <xref:System.Collections.Hashtable>に対応するジェネリック クラスです。

- <xref:System.Collections.ObjectModel.Collection%601> は、 <xref:System.Collections.CollectionBase>に対応するジェネリック クラスです。 <xref:System.Collections.ObjectModel.Collection%601> は基本クラスとして使用できますが、<xref:System.Collections.CollectionBase> とは異なり抽象クラスではないので、使いやすいです。

- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> は、 <xref:System.Collections.ReadOnlyCollectionBase>に対応するジェネリック クラスです。 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> は抽象クラスではなく、既存の <xref:System.Collections.Generic.List%601> を読み取り専用のコレクションとして簡単に公開できるようにするコンストラクターを含んでいます。

- <xref:System.Collections.Generic.Queue%601>、<xref:System.Collections.Concurrent.ConcurrentQueue%601>、<xref:System.Collections.Immutable.ImmutableQueue%601>、<xref:System.Collections.Immutable.ImmutableArray%601>、<xref:System.Collections.Generic.SortedList%602> および <xref:System.Collections.Immutable.ImmutableSortedSet%601> ジェネリック クラスは、同じ名前を持つそれぞれの非ジェネリック クラスに対応しています。

## <a name="additional-types"></a>その他の型

いくつかのジェネリック コレクション型には、対応する非ジェネリック型がありません。 次に例を示します。

- <xref:System.Collections.Generic.LinkedList%601> は、挿入と削除の O(1) 操作を提供する汎用のリンク リストです。

- <xref:System.Collections.Generic.SortedDictionary%602> は、挿入と取得の O(log `n`) 操作で並べ替えられたディクショナリで、 <xref:System.Collections.Generic.SortedList%602>の代替として役立ちます。

- <xref:System.Collections.ObjectModel.KeyedCollection%602> は、リストとディクショナリを組み合わせたもので、独自のキーを含むオブジェクトの格納方法を提供します。

- <xref:System.Collections.Concurrent.BlockingCollection%601> は、境界ブロッキング機能を備えたコレクション クラスを実装します。

- <xref:System.Collections.Concurrent.ConcurrentBag%601> は、順序のない要素の高速な挿入および削除を提供します。

### <a name="immutable-builders"></a>不変ビルダー

<xref:System.Collections.Immutable> 名前空間には、アプリに不変機能が必要な場合に使用できるジェネリック コレクション型があります。 すべての不変コレクション型には、複数の変更を実行しているときのパフォーマンスを最適化する `Builder` クラスがあります。 `Builder` クラスは、変更可能な状態の操作をバッチ処理します。 すべての変更が完了したら、`ToImmutable` メソッドを呼び出してすべてのノードを "凍結" し、<xref:System.Collections.Immutable.ImmutableList%601> などの不変ジェネリック コレクションを作成します。

`Builder` オブジェクトは、非ジェネリック `CreateBuilder()` メソッドを呼び出すことによって作成できます。 `Builder` インスタンスからは `ToImmutable()` を呼び出すことができます。 同様に、`Immutable*` コレクションからは `ToBuilder()` を呼び出して、ジェネリック不変コレクションからビルダー インスタンスを作成できます。 `Builder` のさまざまな型を次に示します。

- <xref:System.Collections.Immutable.ImmutableArray%601.Builder>
- <xref:System.Collections.Immutable.ImmutableDictionary%602.Builder>
- <xref:System.Collections.Immutable.ImmutableHashSet%601.Builder>
- <xref:System.Collections.Immutable.ImmutableList%601.Builder>
- <xref:System.Collections.Immutable.ImmutableSortedDictionary%602.Builder>
- <xref:System.Collections.Immutable.ImmutableSortedSet%601.Builder>

## <a name="linq-to-objects"></a>LINQ to Objects

LINQ to Objects 機能では、オブジェクト型が <xref:System.Collections.IEnumerable?displayProperty=nameWithType> インターフェイスまたは <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> インターフェイスを実装している限り、LINQ クエリを使用してメモリ内オブジェクトにアクセスできます。 LINQ クエリには、データにアクセスする一般的なパターンがあります。通常、これは標準の `foreach` ループよりも簡潔で読みやすく、フィルター処理、並べ替え、およびグループ化機能を備えています。 さらに、LINQ クエリによってパフォーマンスを向上させることができます。 詳細については、「[LINQ to Objects (C#)](../../csharp/programming-guide/concepts/linq/linq-to-objects.md)」、「[LINQ to Objects (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)」、および「[Parallel LINQ (PLINQ)](../parallel-programming/introduction-to-plinq.md)」を参照してください。

## <a name="additional-functionality"></a>その他の機能
一部のジェネリック型には、非ジェネリック コレクション型にはない機能があります。 たとえば、非ジェネリックの <xref:System.Collections.Generic.List%601> クラスに対応する <xref:System.Collections.ArrayList> クラスには、リストを検索するメソッドを指定できる <xref:System.Predicate%601> デリゲートや、リストの各要素に作用するメソッドを表す <xref:System.Action%601> デリゲートや、型間の変換を定義できるようにする <xref:System.Converter%602> デリゲートなどの、汎用デリゲートを受け取るメソッドが多数あります。

<xref:System.Collections.Generic.List%601> クラスを使用すると、リストの並べ替えと検索を行う独自の <xref:System.Collections.Generic.IComparer%601> ジェネリック インターフェイス実装を指定できます。 <xref:System.Collections.Generic.SortedDictionary%602> クラスと <xref:System.Collections.Generic.SortedList%602> クラスにもこの機能があります。 また、これらのクラスを使用すると、コレクションの作成時に比較演算子を指定できます。 同様に、<xref:System.Collections.Generic.Dictionary%602> クラスと <xref:System.Collections.ObjectModel.KeyedCollection%602> クラスを使用すると、独自の等値比較子を指定できます。

## <a name="see-also"></a>関連項目

- [コレクションとデータ構造体](index.md)
- [ 一般的に使用されるコレクション型](commonly-used-collection-types.md)
- [ジェネリック](../generics/index.md)
