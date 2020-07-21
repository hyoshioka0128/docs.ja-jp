---
title: SQL Server Compact および LINQ to SQL
ms.date: 03/30/2017
ms.assetid: 59022359-a5a2-4c42-9a6a-5c0259c3ad17
ms.openlocfilehash: b5a1a12018bd85cf313c1841e6b67ab2edf67b4a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792540"
---
# <a name="sql-server-compact-and-linq-to-sql"></a>SQL Server Compact および LINQ to SQL
SQL Server Compact は、Visual Studio と共にインストールされる既定のデータベースです。 詳しくは、「[SQL Server Compact の使用 (Visual Studio)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/aa983321(v=vs.110))」をご覧ください。  
  
 このトピックでは、使用法、構成、機能セット、および [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のサポートのスコープに関する主要な相違を示します。  
  
## <a name="characteristics-of-sql-server-compact-in-relation-to-linq-to-sql"></a>LINQ to SQL との関係における SQL Server Compact の特徴  
 既定では、SQL Server Compact はすべての Visual Studio エディションでインストールされるため、開発コンピューター上の [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] で使用できます。 ただし、SQL Server Compact と [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] を使用するアプリケーションの配置は、SQL Server アプリケーションの場合とは異なります。 SQL Server Compact は .NET Framework の一部ではないため、アプリケーションにパッケージ化するか、Microsoft サイトから個別にダウンロードする必要があります。  
  
 これには、次のような特徴があります。  
  
- SQL Server Compact は DLL としてパッケージ化されており、データベース ファイル (.sdf 拡張子) に対して直接使用できます。  
  
- SQL Server Compact は、クライアント アプリケーションと同じプロセスで実行されます。 そのため、SQL Server Compact と通信する方が SQL Server と通信するより効率的に優れています。 一方、SQL Server Compact では、コストを伴うマネージド コードとアンマネージド コード間の相互運用性が必要です。  
  
- SQL Server Compact DLL のサイズはわずかです。 このため、アプリケーション全体のサイズが抑制されます。  
  
- [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ランタイムおよび SQLMetal コマンド ライン ツールが SQL Server Compact をサポートしています。  
  
- オブジェクト リレーショナル デザイナーでは SQL Server Compact はサポートされていません。  
  
## <a name="feature-set"></a>機能セット  
 SQL Server Compact の機能セットは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] アプリケーションに影響を及ぼす次の点で、SQL Server の機能セットより単純です。  
  
- SQL Server Compact は、ストアド プロシージャまたはビューをサポートしません。  
  
- SQL Server Compact は、一部のデータ型と SQL 関数のみをサポートします。  
  
- SQL Server Compact は、一部の SQL コンストラクトのみをサポートします。  
  
- SQL Server Compact は、最小限のオプティマイザーを備えています。 クエリによってはタイムアウトする場合もあります。  
  
- SQL Server Compact は、部分信頼をサポートしません。  
  
## <a name="see-also"></a>関連項目

- [参照](reference.md)
