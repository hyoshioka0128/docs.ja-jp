---
title: 初期化式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 98daef1f-15d4-483e-985c-d78ea3abe8c8
ms.openlocfilehash: 5d6656ab77f7ad0f7366a230d98b95cff5b2677b
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854435"
---
# <a name="initialization-expressions"></a>初期化式
初期化式は、新しいオブジェクトを初期化します。 初期化式は、ほとんどの新しい C# 3.0 および Visual Basic 9.0 初期化式を含め、ほとんどがサポートされています。 次の型は、LINQ to Entities クエリによって初期化して返すことができます。  
  
- 0 個以上の型指定されたエンティティ オブジェクトのコレクション、または概念モデルで定義された複合型のプロジェクション。  
  
- Entity Framework でサポートされる CLR 型。
  
- インライン コレクション。  
  
- 匿名型。  
  
 クエリ式構文の次の例では、匿名型の初期化を示します。  
  
 [!code-csharp[DP L2E Conceptual Examples#AnonymousTypeInitialization](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#anonymoustypeinitialization)]
 [!code-vb[DP L2E Conceptual Examples#AnonymousTypeInitialization](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#anonymoustypeinitialization)]  
  
 メソッドベースのクエリ構文の次の例では、匿名型の初期化を示します。  
  
 [!code-csharp[DP L2E Conceptual Examples#AnonymousTypeInitialization_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#anonymoustypeinitialization_mq)]
 [!code-vb[DP L2E Conceptual Examples#AnonymousTypeInitialization_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#anonymoustypeinitialization_mq)]  
  
 ユーザー定義クラスの初期化もサポートされています。 C# 3.0 および Visual Basic 9.0 の初期化パターンがサポートされており、getter と setter のプロパティは対称であることが前提となります。 クエリ式構文の次の例では、クエリ内で初期化されるカスタム クラスを示します。  
  
 [!code-csharp[DP L2E Conceptual Examples#MyOrder](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myorder)]
 [!code-vb[DP L2E Conceptual Examples#MyOrder](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myorder)]  
  
 [!code-csharp[DP L2E Conceptual Examples#TypeInitialization](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#typeinitialization)]
 [!code-vb[DP L2E Conceptual Examples#TypeInitialization](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#typeinitialization)]  
  
 メソッドベース クエリ構文の次の例では、クエリ内で初期化されるカスタム クラスを示します。  
  
 [!code-csharp[DP L2E Conceptual Examples#TypeInitialization_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#typeinitialization_mq)]
 [!code-vb[DP L2E Conceptual Examples#TypeInitialization_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#typeinitialization_mq)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities クエリ内の式](expressions-in-linq-to-entities-queries.md)
