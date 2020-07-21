---
title: グループ結合の実行 (C# での LINQ)
description: C# で LINQ を使用して、グループ結合を実行する方法について説明します。
ms.date: 04/22/2020
ms.assetid: 9667daf9-a5fd-4b43-a5c4-a9c2b744000e
ms.openlocfilehash: 740a861da7dfb9653a874d5baf67eeb2030555b4
ms.sourcegitcommit: 8b02d42f93adda304246a47f49f6449fc74a3af4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82135751"
---
# <a name="perform-grouped-joins"></a>グループ結合の実行

グループ結合は、階層データ構造を作成する場合に便利です。 これは、最初のコレクションの各要素と、2 番目のコレクションの相関関係を持つ要素のセットを組み合わせたものです。

たとえば、`Student` という名前のクラスまたはリレーショナル データベース テーブルに、`Id` と `Name` という 2 つのフィールドが含まれているとします。 `Course` という名前の 2 番目のクラスまたはリレーショナル データベース テーブルには、`StudentId` と `CourseTitle` という 2 つのフィールドが含まれているとします。 この 2 つのデータ ソースのグループ結合は、`Student.Id` と `Course.StudentId` の一致に基づいて、`Course` オブジェクトのコレクションを持つ各 `Student` をグループ化します (コレクションは空の場合もあります)。

> [!NOTE]
> 最初のコレクションの各要素は、2 番目のコレクションに相関関係を持つ要素があるかどうかにかかわらず、グループ結合の結果セットに表示されます。 相関関係を持つ要素が見つからない場合、その要素の相関関係を持つ要素のシーケンスは空です。 そのため、結果セレクターは最初のコレクションのすべての要素にアクセスできます。 これは、非グループ結合の結果セレクターとは異なります。非グループ結合の結果セレクターは、2 番目のコレクションに一致するものがない最初のコレクションの要素にアクセスすることはできません。

> [!WARNING]
> <xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=nameWithType> には、従来のリレーショナル データベースの用語に直接相当するものはありません。 ただし、このメソッドでは内部結合と左外部結合のスーパーセットが実装されます。 これらの操作はどちらも、グループ化結合の観点から記述できます。 詳細については、「[結合操作](../programming-guide/concepts/linq/join-operations.md)」と[「Entity Framework Core」の「GroupJoin」](https://docs.microsoft.com/ef/core/querying/complex-query-operators#groupjoin)を参照してください。

この記事の最初の例では、グループ結合を実行する方法を示します。 2 つ目の例では、グループ結合を使用して XML 要素を作成する方法を示します。

## <a name="example---group-join"></a>例 - グループ結合

次の例では、`Pet.Owner` プロパティと一致する `Person` に基づいて、`Person` 型と `Pet` 型のオブジェクトのグループ結合を実行します。 一致ごとに要素のペアを生成する非グループ結合と異なり、グループ結合は最初のコレクションの要素ごとに 1 つのオブジェクト (この例では `Person` オブジェクト) のみを作成します。 2 番目のコレクションの対応する要素 (この例では `Pet` オブジェクト) が 1 つのコレクションにグループ化されます。 最後に、結果セレクター機能により、`Person.FirstName` と、`Pet` オブジェクトのコレクションで構成される一致ごとに匿名型が作成されます。

[!code-csharp[CsLINQProgJoining#5](~/samples/snippets/csharp/concepts/linq/how-to-perform-grouped-joins_1.cs)]

## <a name="example---group-join-to-create-xml"></a>例 - XML を作成するグループ結合

グループ結合は、LINQ to XML を使用した XML の作成に適しています。 次の例は前の例に似ていますが、匿名型を作成するのではなく、結果セレクター機能により、結合されたオブジェクトを表す XML 要素を作成する点が異なります。

[!code-csharp[CsLINQProgJoining#6](~/samples/snippets/csharp/concepts/linq/how-to-perform-grouped-joins_2.cs)]

## <a name="see-also"></a>関連項目

- <xref:System.Linq.Enumerable.Join%2A>
- <xref:System.Linq.Enumerable.GroupJoin%2A>
- [内部結合の実行](perform-inner-joins.md)
- [左外部結合の実行](perform-left-outer-joins.md)
- [匿名型](../programming-guide/classes-and-structs/anonymous-types.md)
