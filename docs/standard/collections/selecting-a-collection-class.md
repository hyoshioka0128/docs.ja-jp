---
title: コレクション クラスの選択
description: .NET のどのコレクション クラスを選択するかを決定する方法について説明します。 間違った型を使用すると、コレクションの使用が制限されることがあります。
ms.date: 03/18/2019
ms.technology: dotnet-standard
helpviewer_keywords:
- last-in-first-out collections
- first-in-first-out collections
- collections [.NET Framework], selecting collection class
- indexed collections
- Collections classes
- grouping data in collections, selecting collection class
ms.assetid: ba049f9a-ce87-4cc4-b319-3f75c8ddac8a
ms.openlocfilehash: 52a839661a09d6fa7561d67b82d1c1bf854e3cfd
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600816"
---
# <a name="selecting-a-collection-class"></a>コレクション クラスの選択

コレクション クラスは慎重に選択してください。 間違った型を使用すると、コレクションの使用が制限されることがあります。

> [!IMPORTANT]
> 名前空間 <xref:System.Collections> の型は使わないでください。 タイプ セーフの強化やその他の改善があるため、ジェネリックおよび同時実行バージョンのコレクションをお勧めします。

以下の質問を検討します。

- 値が取得された後に要素が通常は破棄されるシーケンシャル リストが必要ですか。

  - そうである場合は、先入れ先出し (FIFO) の動作が必要であれば、<xref:System.Collections.Queue> クラスまたは <xref:System.Collections.Generic.Queue%601> ジェネリック クラスの使用を検討してください。 後入れ先出し (LIFO) の動作が必要であれば、<xref:System.Collections.Stack> クラスまたは <xref:System.Collections.Generic.Stack%601> ジェネリック クラスの使用を検討します。 複数のスレッドから安全にアクセスできるように、同時実行バージョンの <xref:System.Collections.Concurrent.ConcurrentQueue%601> と <xref:System.Collections.Concurrent.ConcurrentStack%601> を使用します。 不変にしたい場合は、不変バージョン、<xref:System.Collections.Immutable.ImmutableQueue%601> および <xref:System.Collections.Immutable.ImmutableStack%601> を検討してください。

  - それ以外の場合は、その他のコレクションの使用を検討してください。

- FIFO や LIFO など特定の順序で要素にアクセスする必要がありますか。またはランダムにアクセスできますか。

  - <xref:System.Collections.Queue> クラス、<xref:System.Collections.Generic.Queue%601>、<xref:System.Collections.Concurrent.ConcurrentQueue%601>、および <xref:System.Collections.Immutable.ImmutableQueue%601> ジェネリック クラスはすべて、FIFO アクセスを提供します。 詳細については、「[スレッド セーフなコレクションを使用する状況](thread-safe/when-to-use-a-thread-safe-collection.md)」をご覧ください。

  - <xref:System.Collections.Stack> クラス、<xref:System.Collections.Generic.Stack%601>、<xref:System.Collections.Concurrent.ConcurrentStack%601>、および <xref:System.Collections.Immutable.ImmutableStack%601> ジェネリック クラスはすべて、LIFO アクセスを提供します。 詳細については、「[スレッド セーフなコレクションを使用する状況](thread-safe/when-to-use-a-thread-safe-collection.md)」をご覧ください。

  - <xref:System.Collections.Generic.LinkedList%601> ジェネリック クラスは、先頭から末尾または末尾から先頭への順次アクセスを可能にします。

- インデックスで各要素にアクセスする必要があるでしょうか。

  - <xref:System.Collections.ArrayList> と <xref:System.Collections.Specialized.StringCollection> クラス、および <xref:System.Collections.Generic.List%601> ジェネリック クラスは、要素の 0 から始まるインデックスによってその要素へのアクセスを提供します。 不変にしたい場合は、不変ジェネリック バージョン、<xref:System.Collections.Immutable.ImmutableArray%601> および <xref:System.Collections.Immutable.ImmutableList%601> を検討してください。

  - <xref:System.Collections.Hashtable>、<xref:System.Collections.SortedList>、<xref:System.Collections.Specialized.ListDictionary>、<xref:System.Collections.Specialized.StringDictionary> クラス、および <xref:System.Collections.Generic.Dictionary%602>、<xref:System.Collections.Generic.SortedDictionary%602> ジェネリック クラスは、要素のキーによってその要素へのアクセスを提供します。 また、いくつかの対応する型に、<xref:System.Collections.Immutable.ImmutableHashSet%601>、<xref:System.Collections.Immutable.ImmutableDictionary%602>、<xref:System.Collections.Immutable.ImmutableSortedSet%601>、および <xref:System.Collections.Immutable.ImmutableSortedDictionary%602> の不変バージョンがあります。

  - <xref:System.Collections.Specialized.NameObjectCollectionBase> と <xref:System.Collections.Specialized.NameValueCollection> クラス、および <xref:System.Collections.ObjectModel.KeyedCollection%602> と <xref:System.Collections.Generic.SortedList%602> ジェネリック クラスは、要素の 0 から始まるインデックスまたはキーのいずれかによって、その要素へのアクセスを提供します。

- 各要素に含まれることになるのは、1 つの値、1 つのキーと 1 つの値の組み合わせ、または 1 つのキーと複数の値の組み合わせのどれですか。

  - 1 つの値: <xref:System.Collections.IList> インターフェイスまたは <xref:System.Collections.Generic.IList%601> ジェネリック インターフェイスに基づくいずれかのコレクションを使用します。 不変のオプションについては、<xref:System.Collections.Immutable.IImmutableList%601> ジェネリック インターフェイスを検討してください。

  - 1 つのキーと 1 つの値: <xref:System.Collections.IDictionary> インターフェイスまたは <xref:System.Collections.Generic.IDictionary%602> ジェネリック インターフェイスに基づくいずれかのコレクションを使用します。 不変のオプションについては、<xref:System.Collections.Immutable.IImmutableSet%601> または <xref:System.Collections.Immutable.IImmutableDictionary%602> のジェネリック インターフェイスを検討してください。

  - キーが埋め込まれた 1 つの値: <xref:System.Collections.ObjectModel.KeyedCollection%602> ジェネリック クラスを使用します。

  - 複数の値を持つ 1 つのキー: <xref:System.Collections.Specialized.NameValueCollection> クラスを使用します。

- 要素を入力されたときとは異なる方法で並べ替える必要がありますか。

  - <xref:System.Collections.Hashtable> クラスは、ハッシュ コードによってその要素を並べ替えます。

  - <xref:System.Collections.SortedList> クラスと、<xref:System.Collections.Generic.SortedList%602> および <xref:System.Collections.Generic.SortedDictionary%602> ジェネリック クラスでは、キーによってその要素を並べ替えます。 並べ替え順序は、<xref:System.Collections.SortedList> クラスの <xref:System.Collections.IComparer> インターフェイスの実装と、<xref:System.Collections.Generic.SortedList%602> および <xref:System.Collections.Generic.SortedDictionary%602> ジェネリック クラスの <xref:System.Collections.Generic.IComparer%601> ジェネリック インターフェイスの実装に基づきます。 この 2 つのジェネリック型のうち、<xref:System.Collections.Generic.SortedDictionary%602> は <xref:System.Collections.Generic.SortedList%602> よりもパフォーマンスに優れていますが、メモリ消費は <xref:System.Collections.Generic.SortedList%602> の方が少なくなります。

  - <xref:System.Collections.ArrayList> は、<xref:System.Collections.IComparer> 実装をパラメーターとして受け取る、<xref:System.Collections.ArrayList.Sort%2A> メソッドを提供します。 それに対応するジェネリックである <xref:System.Collections.Generic.List%601> ジェネリック クラスは、<xref:System.Collections.Generic.IComparer%601> ジェネリック インターフェイスの実装をパラメーターとして受け取る、<xref:System.Collections.Generic.List%601.Sort%2A> メソッドを提供します。

- 高速な検索と情報の取得が必要ですか。

  - <xref:System.Collections.Specialized.ListDictionary> は、小規模なコレクション (10 個以下のアイテム) では <xref:System.Collections.Hashtable> より高速です。 <xref:System.Collections.Generic.Dictionary%602> ジェネリック クラスは、<xref:System.Collections.Generic.SortedDictionary%602> ジェネリック クラスよりも高速の参照を提供します。 マルチスレッドの実装は <xref:System.Collections.Concurrent.ConcurrentDictionary%602> です。 <xref:System.Collections.Concurrent.ConcurrentBag%601> は、順序指定されていないデータのために、高速なマルチスレッドの挿入を提供します。 両方のマルチスレッドのタイプについては、「[スレッド セーフなコレクションを使用する状況](thread-safe/when-to-use-a-thread-safe-collection.md)」を参照してください。

- 文字列だけを受け入れるコレクションは必要ですか。

  - <xref:System.Collections.Specialized.StringCollection> (<xref:System.Collections.IList> に基づく) および <xref:System.Collections.Specialized.StringDictionary> (<xref:System.Collections.IDictionary> に基づく) は、<xref:System.Collections.Specialized> 名前空間にあります。

  - さらに、ジェネリック型の引数として <xref:System.String> クラスを指定することにより、<xref:System.Collections.Generic> 名前空間にある任意のジェネリック コレクション クラスを厳密に型指定された文字列コレクションとして使用できます。 たとえば、[List\<String>](xref:System.Collections.Generic.List%601) または [Dictionary<String,String>](xref:System.Collections.Generic.Dictionary%602) 型の変数を宣言することができます。

## <a name="linq-to-objects-and-plinq"></a>LINQ to Objects および PLINQ

LINQ to Objects により、開発者は、オブジェクト型で <xref:System.Collections.IEnumerable> または <xref:System.Collections.Generic.IEnumerable%601> を実装している限り、LINQ クエリを使用してインメモリ オブジェクトにアクセスできます。 LINQ クエリはデータ アクセス用の一般的なパターンです。通常、これは標準の `foreach` ループよりも簡潔で読みやすく、フィルター処理、並べ替え、およびグループ化機能を備えています。 詳細については、「[LINQ to Objects (C#)](../../csharp/programming-guide/concepts/linq/linq-to-objects.md)」および「[LINQ to Objects (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)」を参照してください。

PLINQ は、マルチコア コンピューターをより効率的に使用することにより、多くのシナリオでより高速にクエリを実行できる LINQ to Objects の並列実装を提供します。 詳細については、「[Parallel LINQ (PLINQ)](../parallel-programming/introduction-to-plinq.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Collections>
- <xref:System.Collections.Specialized>
- <xref:System.Collections.Generic>
- [スレッドセーフなコレクション](thread-safe/index.md)
