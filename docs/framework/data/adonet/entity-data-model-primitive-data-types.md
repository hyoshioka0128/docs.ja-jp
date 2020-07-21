---
title: Entity Data Model:プリミティブ データ型
ms.date: 03/30/2017
ms.assetid: 7635168e-0566-4fdd-8391-7941b0d9f787
ms.openlocfilehash: dd688a06a47f4c44c27ddee2120b9de6980672fc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795163"
---
# <a name="entity-data-model-primitive-data-types"></a>Entity Data Model:プリミティブ データ型
Entity Data Model (EDM) では、概念モデルで[プロパティ](property.md)を定義するために使用する一連の抽象プリミティブ データ型 (String、Boolean、Int32 など) がサポートされています。 これらのプリミティブ データ型は、SQL Server データベースや共通言語ランタイム (CLR) などのストレージ環境またはホスト環境でサポートされる、実際のプリミティブ データ型のプロキシです。 EDM では、プリミティブ データ型に対する演算や変換のセマンティクスを定義していません。これらのセマンティクスは、ストレージ環境またはホスト環境で定義されます。 通常、EDM のプリミティブ データ型は、ストレージ環境またはホスト環境の対応プリミティブ データ型にマップされます。 Entity Framework で EDM のプリミティブ型が SQL Server データ型にマップされる方法については、「[Entity Framework 用 SqlClient の型](./ef/sqlclient-for-ef-types.md)」をご覧ください。  
  
> [!NOTE]
> EDM では、プリミティブ データ型のコレクションをサポートしていません。  
  
 EDM の構造化データ型について詳しくは、「[エンティティ型](entity-type.md)」と「[複合型](complex-type.md)」をご覧ください。  
  
## <a name="primitive-data-types-supported-in-the-entity-data-model"></a>Entity Data Model でサポートされるプリミティブ データ型  
 下の表は、EDM でサポートされるプリミティブ データ型の一覧を示します。 さらに、各プリミティブ データ型に使用できる[ファセット](facet.md)も示されています。  
  
|プリミティブ データ型|説明|使用できるファセット|  
|-------------------------|-----------------|-----------------------|  
|2 項|バイナリ データを格納します。|MaxLength、FixedLength、Nullable、Default|  
|ブール型|`true` または `false` の値を格納します。|Nullable、Default|  
|Byte|符号なし 8 ビット整数値を格納します。|Precision、Nullable、Default|  
|DateTime|日時を表します。|Precision、Nullable、Default|  
|DateTimeOffset|GMT からのオフセット (分単位) としての日時を格納します。|Precision、Nullable、Default|  
|Decimal (10 進数型)|有効桁数と小数点以下桁数が固定長の数値を格納します。|Precision、Nullable、Default|  
|Double|15 桁の有効桁数を持つ浮動小数点数を格納します。|Precision、Nullable、Default|  
|Float|7 桁の有効桁数を持つ浮動小数点数を格納します。|Precision、Nullable、Default|  
|GUID|16 バイトの一意識別子を格納します。|Precision、Nullable、Default|  
|Int16|符号付き 16 ビット整数値を格納します。|Precision、Nullable、Default|  
|Int32|符号付き 32 ビット整数値を格納します。|Precision、Nullable、Default|  
|Int64|符号付き 64 ビット整数値を格納します。|Precision、Nullable、Default|  
|SByte|符号付き 8 ビット整数値を格納します。|Precision、Nullable、Default|  
|String|文字データを格納します。|Unicode、FixedLength、MaxLength、Collation、Precision、Nullable、Default|  
|時刻|時刻を格納します。|Precision、Nullable、Default|  
  
## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
