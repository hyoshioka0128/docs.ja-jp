---
title: コマンドを使用したデータ変更
ms.date: 03/30/2017
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.openlocfilehash: 34c73549f18cd4bebb8caf842b252828b7f0a185
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780567"
---
# <a name="using-commands-to-modify-data"></a>コマンドを使用したデータ変更
.NET Framework データ プロバイダーを使用すると、ストアド プロシージャまたはデータ定義言語のステートメント (たとえば、CREATE TABLE、ALTER COLUMN など) を実行して、データベースやカタログに対するスキーマ操作を実行できます。 これらのコマンドはクエリとは異なり、行を返さないため、**Command** オブジェクトではこれらを処理するために **ExecuteNonQuery** が提供されています。  
  
 **ExecuteNonQuery** メソッドを使用すると、スキーマを変更できるだけでなく、データを変更するが行を返さない INSERT、UPDATE、DELETE などの SQL ステートメントも処理できます。  
  
 **ExecuteNonQuery** メソッドでは行は返されませんが、**Command** オブジェクトの **Parameters** コレクションを通じて入力パラメーター、出力パラメーター、および戻り値を受け渡しできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [データ ソースのデータの更新](updating-data-in-a-data-source.md)  
 データベース内のデータを変更するコマンドまたはストアド プロシージャを実行する方法について説明します。  
  
 [カタログ操作の実行](performing-catalog-operations.md)  
 データベース スキーマを変更するコマンドを実行する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [コマンドおよびパラメーター](commands-and-parameters.md)
- [ADO.NET の概要](ado-net-overview.md)
