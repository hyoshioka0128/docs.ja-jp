---
title: '方法: 行セットを返す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 725718f5-da29-4841-9f53-aafef64ba977
ms.openlocfilehash: b853a6f2175009cbcbc01c14a6732b98e37e1a7f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003061"
---
# <a name="how-to-return-rowsets"></a>方法: 行セットを返す
この例では、データベースから行セットを返し、入力パラメーターを使用して結果をフィルター処理します。  
  
 行セットを返すストアド プロシージャを実行する場合は、ストアド プロシージャからの戻り値を格納する "*結果*" クラスを使用します。 詳しくは、「[LINQ to SQL のソース コードの分析](analyzing-linq-to-sql-source-code.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の例は、顧客の行を返し、入力パラメーターを使用して、顧客が在住する市が "London" である行のみを返すストアド プロシージャを示しています。 例では、列挙可能な `CustomersByCityResult` クラスを想定しています。  
  
```sql  
CREATE PROCEDURE [dbo].[Customers By City]  
    (@param1 NVARCHAR(20))  
AS  
BEGIN  
    -- SET NOCOUNT ON added to prevent extra result sets from  
    -- interfering with SELECT statements.  
    SET NOCOUNT ON;  
    SELECT CustomerID, ContactName, CompanyName, City from Customers  
        as c where c.City=@param1  
END  
```  
  
 [!code-csharp[DLinqSprox#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#1)]
 [!code-vb[DLinqSprox#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [ストアド プロシージャ](stored-procedures.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
