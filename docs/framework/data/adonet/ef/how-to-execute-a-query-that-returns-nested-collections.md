---
title: '方法: 入れ子になったコレクションを返すクエリを実行する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f7f385f3-ffcf-4f3b-af35-de8818938e5f
ms.openlocfilehash: 87bd7124d476ef39553db3ceaca206e44db8e5e9
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854619"
---
# <a name="how-to-execute-a-query-that-returns-nested-collections"></a>方法: 入れ子になったコレクションを返すクエリを実行する
ここでは、<xref:System.Data.EntityClient.EntityCommand> オブジェクトを使用して概念モデルに対してコマンドを実行する方法、および <xref:System.Data.EntityClient.EntityDataReader> を使用して入れ子になったコレクションの結果を取得する方法について説明します。  
  
### <a name="to-run-the-code-in-this-example"></a>この例のコードを実行するには  
  
1. [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) をプロジェクトに追加し、Entity Framework が使用されるようにプロジェクトを構成します。 詳細については、[Entity Data Model ウィザードを使用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))」を参照してください。  
  
2. アプリケーションのコード ページで、次の `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a>例  
 "*入れ子になったコレクション*" とは、別のコレクションに含まれているコレクションのことです。 次に示すコードでは、`Contacts` のコレクションと、それぞれの `SalesOrderHeaders` に関連付けられている、`Contact` の入れ子になったコレクションを取得します。  
  
 [!code-csharp[DP EntityServices Concepts#ReturnNestedCollectionWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#returnnestedcollectionwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ReturnNestedCollectionWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#returnnestedcollectionwithentitycommand)]  
  
## <a name="see-also"></a>関連項目

- [Entity Framework 用の EntityClient プロバイダー](entityclient-provider-for-the-entity-framework.md)
