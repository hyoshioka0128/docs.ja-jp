---
title: データベースからの単一の値の取得
description: ADO.NET で単一の値を返す方法について説明します。 このコード例は、挿入されたレコードの ID 列の値を返します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
ms.openlocfilehash: a6f268f72f8b8a09ae48ba3cad6254323cb95a20
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286703"
---
# <a name="obtaining-a-single-value-from-a-database"></a>データベースからの単一の値の取得
テーブルやデータ ストリームの形式ではなく、単に 1 つの値をデータベース情報として返すことが必要な場合があります。 たとえば、COUNT(\*)、SUM(Price)、AVG(Quantity) などの集計関数の結果を返す場合です。 **Command** オブジェクトでは、**ExecuteScalar** メソッドを使用して単一の値を返す機能が提供されています。 **ExecuteScalar** メソッドでは、結果セットの 1 行目の 1 列目の値がスカラー値として返されます。  
  
 <xref:System.Data.SqlClient.SqlCommand> を使用して新しい値をデータベースに挿入するコード サンプルを次に示します。 挿入したレコードの ID 列の値を取得するために、<xref:System.Data.SqlClient.SqlCommand.ExecuteScalar%2A> メソッドが使用されています。  
  
 [!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlCommand.ExecuteScalar/CS/source.cs#1)]
 [!code-vb[DataWorks SqlCommand.ExecuteScalar#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlCommand.ExecuteScalar/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [コマンドおよびパラメーター](commands-and-parameters.md)
- [コマンドの実行](executing-a-command.md)
- [DbConnection、DbCommand、および DbException](dbconnection-dbcommand-and-dbexception.md)
- [ADO.NET の概要](ado-net-overview.md)
