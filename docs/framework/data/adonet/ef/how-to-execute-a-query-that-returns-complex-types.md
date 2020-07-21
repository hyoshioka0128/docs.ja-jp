---
title: '方法: 複合型を返すクエリを実行する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c2209fdb-70ef-4dea-8bb8-097fe96f5563
ms.openlocfilehash: b08b220e969ad1c400413978c85b2f107d64a688
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854646"
---
# <a name="how-to-execute-a-query-that-returns-complex-types"></a>方法: 複合型を返すクエリを実行する
このトピックでは、複合型プロパティを含むエンティティ型オブジェクトを返す [!INCLUDE[esql](../../../../../includes/esql-md.md)] クエリを実行する方法について説明します。  
  
### <a name="to-run-the-code-in-this-example"></a>この例のコードを実行するには  
  
1. [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) をプロジェクトに追加し、Entity Framework が使用されるようにプロジェクトを構成します。 詳細については、[Entity Data Model ウィザードを使用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))」を参照してください。  
  
2. アプリケーションのコード ページで、次の `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3. .edmx ファイルをダブルクリックして、エンティティ デザイナーの [[モデル ブラウザー] ウィンドウ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738483(v=vs.100))にモデルを表示します。 エンティティ デザイナー画面で、`Contact` エンティティ型の `Email` プロパティと `Phone` プロパティを選択し、右クリックして **[新しい複合型へのリファクター]** を選択します。  
  
4. 選択した `Email` プロパティと `Phone` プロパティの新しい複合型が**モデル ブラウザー**に追加されます。 複合型には既定の名前が設定されます。 **[プロパティ]** ウィンドウで型の名前を `EmailPhone` に変更します。 また、新しい `ComplexProperty` プロパティが `Contact` エンティティ型に追加されます。 プロパティの名前を `EmailPhoneComplexType.` に変更します。  
  
     Entity Data Model ウィザードを使用した複合型の作成と変更について詳しくは、「[方法: 既存のプロパティを複合型プロパティにリファクタリングする](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456814(v=vs.100))」および「[方法: 複合型を作成および変更する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456820(v=vs.100))」をご覧ください。  
  
## <a name="example"></a>例  
 次の例では、`Contact` オブジェクトのコレクションを返し、`Contact` オブジェクトの 2 つのプロパティである `ContactID` と `EmailPhoneComplexType` 複合型の値を表示するクエリを実行します。  
  
 [!code-csharp[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#complextypewithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#complextypewithentitycommand)]
