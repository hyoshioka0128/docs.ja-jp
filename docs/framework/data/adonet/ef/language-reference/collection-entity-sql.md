---
title: COLLECTION (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 03228bfa-be3a-4ccc-82f8-eee429f85cf1
ms.openlocfilehash: 5a1af1aab8a084b19e48fbdbb159d7ddd8a8dd7c
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73039905"
---
# <a name="collection-entity-sql"></a>COLLECTION (Entity SQL)
COLLECTION キーワードは、インライン関数を定義する場合にのみ使用します。 コレクション関数は、値のコレクションを操作してスカラー出力を生成する関数です。  
  
## <a name="syntax"></a>構文  
  
```csharp  
COLLECTION(type_definition)
```  
  
## <a name="arguments"></a>引数  
 `type_definition`  
 サポートされる型、行、または参照のコレクションを返す式。  
  
## <a name="remarks"></a>Remarks  
 COLLECTION キーワードについて詳しくは、「 [Type Definitions](type-definitions-entity-sql.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の例は、COLLECTION キーワードを使用して 10 進数のコレクションをインライン クエリ関数の引数として宣言する方法を示します。  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
