---
title: Oracle および ADO.NET
description: .NET Framework Data Provider for Oracle の機能と動作について説明します。これは、Oracle Call Interface を使用して、Oracle データベースへのアクセスを提供します。
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ee8e389-53cf-45cf-80bd-1df63ef34f2e
ms.openlocfilehash: 8757352a7444fad802ea88ba58e0fe643c86cbb8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286690"
---
# <a name="oracle-and-adonet"></a>Oracle および ADO.NET
> [!NOTE]
> <xref:System.Data.OracleClient> の型は非推奨になっています。 これらの型は、.NET Framework の現在のバージョンでは引き続きサポートされていますが、今後のリリースでは削除される予定です。 サードパーティの Oracle プロバイダーを使用することをお勧めします。  
  
 このセクションでは、.NET Framework Data Provider for Oracle 固有の機能および動作について説明します。  
  
 .NET Framework Data Provider for Oracle では、Oracle Client ソフトウェアとして提供されている Oracle Call Interface (OCI) を使用して Oracle データベースにアクセスできます。 このデータ プロバイダーの機能は、SQL Server、OLE DB、ODBC に対する .NET Framework データ プロバイダーの機能と同等になるように設計されています。  
  
 .NET Framework Data Provider for Oracle を使用するには、アプリケーションで以下のように <xref:System.Data.OracleClient> 名前空間を参照する必要があります。  
  
```vb  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data.OracleClient;  
```  
  
 コードをコンパイルするには、DLL への参照も必要です。 たとえば、C# プログラムをコンパイルする場合、コマンド ラインに以下のコードを含める必要があります。  
  
```console
csc /r:System.Data.OracleClient.dll  
```  
  
## <a name="in-this-section"></a>このセクションの内容  
 [システム要件](system-requirements-for-the-dotnet-data-provider-for-oracle.md)  
 .NET Framework Data Provider for Oracle を使用するための要件を説明し、その際に知っておくべきさまざまなことについて説明します。  
  
 [Oracle BFILE](oracle-bfiles.md)  
 <xref:System.Data.OracleClient.OracleBFile> クラスについて説明します。このクラスは、Oracle BFILE データ型を操作するために使用されます。  
  
 [Oracle LOB](oracle-lobs.md)  
 <xref:System.Data.OracleClient.OracleLob> クラスについて説明します。このクラスは、Oracle LOB データ型を操作するために使用されます。  
  
 [Oracle REF CURSOR](oracle-ref-cursors.md)  
 Oracle REF CURSOR データ型のサポートについて説明します。  
  
 [OracleTypes](oracletypes.md)  
 <xref:System.Data.OracleClient.OracleNumber> や <xref:System.Data.OracleClient.OracleString> など、Oracle データ型を操作するために使用する構造体について説明します。  
  
 [Oracle シーケンス](oracle-sequences.md)  
 サーバーによって生成されたキー値 (Oracle シーケンス) を取得するためのサポートについて説明します。  
  
 [Oracle データ型のマッピング](oracle-data-type-mappings.md)  
 Oracle データ型およびその <xref:System.Data.OracleClient.OracleDataReader> へのマップを一覧表示します。  
  
 [Oracle 分散トランザクション](oracle-distributed-transactions.md)  
 <xref:System.Data.OracleClient.OracleConnection> オブジェクトが、トランザクションがアクティブであると判断した場合に、既存の分散トランザクションに自動的に参加する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ADO.NET アプリケーションのセキュリティ保護](securing-ado-net-applications.md)  
 ADO.NET を使用する場合の安全なコーディング方法について説明します。  
  
 [DataSet、DataTable、および DataView](./dataset-datatable-dataview/index.md)  
 `DataSets`、型指定された `DataSets`、`DataTables`、および `DataViews` の作成方法と使用方法について説明します。  
  
 [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)  
 ADO.NET でのデータの操作方法について説明します。  
  
 [SQL Server と ADO.NET](./sql/index.md)  
 SQL Server 固有の機能の使用方法について説明します。  
  
 [DbProviderFactories](dbproviderfactories.md)  
 ADO.NET でプロバイダーに依存しないコードを記述するための Generic クラスについて説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET](index.md)
- [ADO.NET の概要](ado-net-overview.md)
