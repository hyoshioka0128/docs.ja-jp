---
title: '方法: LINQ の結合を使用してデータを結合する'
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], joins
- joins [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- Group Join clause [Visual Basic]
- joining [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 5b00a478-035b-41c6-8918-be1a97728396
ms.openlocfilehash: de8c4ec3ab8a0f2335c034231c661380420fd31b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405005"
---
# <a name="how-to-combine-data-with-linq-by-using-joins-visual-basic"></a>方法: LINQ の結合を使用してデータを結合する (Visual Basic)
Visual Basic では、コレクション間の共通値に基づいて複数のコレクションの内容を結合できるようにするための、`Join` および `Group Join` クエリ句が提供されます。 これらの値は "*キー*" 値と呼ばれます。 リレーショナル データベースの概念をよく理解している開発者は、`Join` 句を内部結合として認識し、`Group Join` 句を実質的に左外部結合として認識します。  
  
 このトピックの例では、`Join` と `Group Join` のクエリ句を使用してデータを結合するいくつかの方法を示します。  
  
## <a name="create-a-project-and-add-sample-data"></a>プロジェクトを作成してサンプル データを追加する  
  
#### <a name="to-create-a-project-that-contains-sample-data-and-types"></a>サンプルのデータと種類を含むプロジェクトを作成するには  
  
1. このトピックのサンプルを実行するには、Visual Studio を開き、新しい Visual Basic コンソール アプリケーションのプロジェクトを追加します。 Visual Basic によって作成された Module1.vb ファイルをダブルクリックします。  
  
2. このトピックのサンプルでは、次のコード例の `Person` および `Pet` という種類とデータを使用します。 Visual Basic によって作成された既定の `Module1` モジュールに、このコードをコピーします。  
  
     [!code-vb[VbLINQHowTos#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#1)]  
    [!code-vb[VbLINQHowTos#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#2)]  
  
## <a name="perform-an-inner-join-by-using-the-join-clause"></a>Join 句を使用して内部結合を実行する  
 内部結合では、2 つのコレクションのデータを結合します。 指定されたキー値が一致する項目が含まれます。 いずれかのコレクションの項目のうち、他のコレクションに一致する項目がないものは除外されます。  
  
 Visual Basic では、LINQ で内部結合を実行するためのオプションとして、暗黙的な結合と明示的な結合という 2 つが提供されます。  
  
 暗黙的な結合では、`From` 句で結合されるコレクションを指定し、`Where` 句で一致するキー フィールドを識別します。 Visual Basic では、指定されたキー フィールドに基づいて、2 つのコレクションを暗黙的に結合します。  
  
 結合で使用するキー フィールドを特定する場合は、`Join` 句を使用して明示的な結合を指定できます。 この場合も、`Where` 句を使用してクエリ結果をフィルター処理できます。  
  
#### <a name="to-perform-an-inner-join-by-using-the-join-clause"></a>Join 句を使用して内部結合を実行するには  
  
1. 次のコードをプロジェクトの `Module1` モジュールに追加して、暗黙的および明示的な内部結合の両方の例を確認します。  
  
     [!code-vb[VbLINQHowTos#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#4)]  
  
## <a name="perform-a-left-outer-join-by-using-the-group-join-clause"></a>Group Join 句を使用して左外部結合を実行する  
 左外部結合には、結合の左側のコレクションのすべての項目と、結合の右側のコレクションで一致する値のみが含まれます。 左側のコレクションに一致する項目がない、結合の右側のコレクションの項目はすべて、クエリ結果から除外されます。  
  
 `Group Join` 句では、実際には左外部結合を実行します。 通常は左外部結合と呼ばれるものと、`Group Join` 句で返されるものの違いは、`Group Join` 句では、左側のコレクションの項目ごとに、結合の右側のコレクションからの結果がグループ化されることです。 リレーショナル データベースでは、左外部結合でグループ化されていない結果が返されます。この場合、クエリ結果の各項目には、結合の両方のコレクションの一致する項目が含まれます。 この場合、結合の左側のコレクションの項目が、右側のコレクションの一致する項目ごとに繰り返されます。 次の手順を完了すると、このようになるのがわかります。  
  
 クエリを拡張してグループ化されたクエリ結果ごとに 1 つの項目を返すようにすることで、`Group Join` クエリの結果をグループ化されていない結果として取得できます。 そのためには、グループ化されたコレクションの `DefaultIfEmpty` メソッドに対してクエリを確実に実行する必要があります。 これにより、右側のコレクションに一致する結果がない場合でも、確実に結合の左側のコレクションの項目がクエリ結果に引き続き含まれるようになります。 結合の右側のコレクションに一致する値がない場合は、クエリにコードを追加して既定の結果値を指定できます。  
  
#### <a name="to-perform-a-left-outer-join-by-using-the-group-join-clause"></a>Group Join 句を使用して左外部結合を実行するには  
  
1. 次のコードをプロジェクトの `Module1` モジュールに追加して、グループ化された左外部結合とグループ化されていない左外部結合の両方の例を確認します。  
  
     [!code-vb[VbLINQHowTos#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#3)]  
  
## <a name="perform-a-join-by-using-a-composite-key"></a>複合キーを使用して結合を実行する  
 `Join` または `Group Join` 句で `And` キーワードを使用すると、結合されるコレクションの値を照合するときに使用する複数のキー フィールドを識別できます。 `And` キーワードでは、結合される項目について、指定されたすべてのキー フィールドが一致する必要があることを指定します。  
  
#### <a name="to-perform-a-join-by-using-a-composite-key"></a>複合キーを使用して結合を実行するには  
  
1. 次のコードをプロジェクトの `Module1` モジュールに追加して、複合キーを使用する結合の例を確認します。  
  
     [!code-vb[VbLINQHowTos#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#5)]  
  
## <a name="run-the-code"></a>コードを実行する  
  
#### <a name="to-add-code-to-run-the-examples"></a>例を実行するコードを追加するには  
  
1. プロジェクトの `Module1` モジュールの `Sub Main` を次のコードに置き換えて、このトピックの例を実行します。  
  
     [!code-vb[VbLINQHowTos#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#6)]  
  
2. F5 キーを押して例を実行します。  
  
## <a name="see-also"></a>関連項目

- [LINQ](index.md)
- [Visual Basic における LINQ の概要](introduction-to-linq.md)
- [Join 句](../../../language-reference/queries/join-clause.md)
- [Group Join 句](../../../language-reference/queries/group-join-clause.md)
- [From 句](../../../language-reference/queries/from-clause.md)
- [WHERE 句](../../../language-reference/queries/where-clause.md)
- [クエリ](../../../language-reference/queries/index.md)
- [LINQ によるデータ変換 (C#)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)
