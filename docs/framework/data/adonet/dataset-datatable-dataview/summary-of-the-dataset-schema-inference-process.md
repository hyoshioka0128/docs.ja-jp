---
title: DataSet スキーマの推論プロセスの概要
ms.date: 03/30/2017
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
ms.openlocfilehash: 35e9b67d2d0a47aa69eabdb4b7e94f95b0b9589f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833978"
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>DataSet スキーマの推論プロセスの概要
推論プロセスでは、まず、テーブルとして推論する XML ドキュメントの要素を決定します。 XML ドキュメントの残りの要素から、それらのテーブルの列が推論によって決定されます。 入れ子状のテーブルの場合は、入れ子になった <xref:System.Data.DataRelation> オブジェクトと <xref:System.Data.ForeignKeyConstraint> オブジェクトが生成されます。  
  
 推論規則について、次に簡単に説明します。  
  
- 属性を持つ要素は、テーブルとして推論されます。  
  
- 子要素を持つ要素は、テーブルとして推論されます。  
  
- 繰り返し出現する要素は、単一のテーブルとして推論されます。  
  
- ドキュメント (ルート) 要素に属性がなく、列として推論される子要素もない場合、その要素は <xref:System.Data.DataSet> として推論されます。 それ以外の場合は、ドキュメント要素はテーブルとして推論されます。  
  
- 属性は、列として推論されます。  
  
- 属性または子要素を持たず、繰り返し出現することもない要素は、列として推論されます。  
  
- テーブルとして推論される要素が、同じくテーブルとして推論される他の要素の内部に入れ子になっている場合は、その 2 つのテーブル間に入れ子になった **DataRelation** が作成されます。 その場合、**TableName_Id** という名前の新しい主キー列がその両方のテーブルに追加され、**DataRelation** によって使用されます。 この **TableName_Id** 列を使用して、この 2 つのテーブル間に **ForeignKeyConstraint** が作成されます。  
  
- テーブルとして推論される要素に、テキストは含まれているが子要素は含まれていない場合は、**TableName_Text** という名前の新しい列が各要素のテキストに作成されます。 テーブルとして推論される要素にテキストだけでなく、子要素もある場合、テキストは無視されます。  
  
## <a name="see-also"></a>関連項目

- [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)
- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
