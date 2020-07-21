---
title: side-by-side 実行
ms.date: 03/30/2017
ms.assetid: 9f9ba96d-9f89-4f65-bb2f-6860879f4393
ms.openlocfilehash: a624aac2ed1f3ab124973c84bc74e39297600c8b
ms.sourcegitcommit: 19014f9c081ca2ff19652ca12503828db8239d48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980016"
---
# <a name="side-by-side-execution-in-adonet"></a>ADO.NET での side-by-side 実行
.NET Framework の side-by-side 実行は、.NET Framework の複数のバージョンがインストールされている 1 台のコンピューター上で、アプリケーションのコンパイル時のバージョンのみを使用して、アプリケーションを実行する機能です。 side-by-side 実行について詳しくは、[side-by-side 実行](../../deployment/side-by-side-execution.md)に関する記事をご覧ください。  
  
 あるバージョンの .NET Framework を使用してコンパイルされたアプリケーションを、別のバージョンの .NET Framework で実行することもできます。 ただし、インストールされている .NET Framework のバージョンごとにアプリケーションをコンパイルして、各バージョンを別々に実行することをお勧めします。 いずれの場合でも、ADO.NET の各リリース間の変更によって生じるアプリケーションの上位互換性または下位互換性の問題に注意する必要があります。  
  
## <a name="forward-compatibility-and-backward-compatibility"></a>上位互換性と下位互換性  
 上位互換性とは、.NET Framework の旧バージョンでコンパイルしたアプリケーションが、新しいバージョンの .NET Framework でも実行できることを意味します。 .NET Framework バージョン 1.1 用に書かれた ADO.NET のコードは、後のバージョンとの上位互換性があります。  
  
 下位互換性とは、アプリケーションが新しいバージョンの .NET Framework 用にコンパイルされていても、機能を低下させずに、.NET Framework の以前のバージョンで引き続き実行できることを意味します。 当然のことながら、.NET Framework の新しいバージョンで導入された機能については、これは該当しません。  
  
## <a name="the-net-framework-data-provider-for-odbc"></a>.NET Framework Data Provider for ODBC  
 バージョン 1.1 以降の .NET Framework には、.NET Framework Data Provider for ODBC (<xref:System.Data.Odbc>) が含まれています。
  
 ODBC データ プロバイダーを使用してデータ ソースに接続する、.NET Framework バージョン 1.0 用に開発されたアプリケーションを、.NET Framework バージョン 1.1 以降で実行する場合は、ODBC データ プロバイダーの名前空間を **System.Data.Odbc** に更新する必要があります。 その後で、.NET Framework の新しいバージョン用に再コンパイルする必要があります。  
  
 ODBC データ プロバイダーを使用してデータ ソースに接続する .NET Framework バージョン 2.0 以降用に開発されたアプリケーションを、.NET Framework バージョン 1.0 で実行する場合は、ODBC データ プロバイダーをダウンロードし、.NET Framework バージョン 1.0 システムにインストールする必要があります。 次に、ODBC データ プロバイダーの名前空間を **Microsoft.Data.Odbc** に変更し、アプリケーションを .NET Framework バージョン 1.0 用に再コンパイルする必要があります。  
  
## <a name="the-net-framework-data-provider-for-oracle"></a>.NET Framework Data Provider for Oracle  
 バージョン 1.1 以降の .NET Framework には、.NET Framework Data Provider for Oracle (<xref:System.Data.OracleClient>) が含まれています。
  
 データ プロバイダーを使用してデータ ソースに接続する .NET Framework バージョン 2.0 以降用に開発されたアプリケーションを、.NET Framework バージョン 1.0 で実行する場合は、データ プロバイダーをダウンロードし、.NET Framework バージョン 1.0 システムにインストールする必要があります。  
  
## <a name="code-access-security"></a>コード アクセス セキュリティ  
 .NET Framework バージョン 1.0 の .NET Framework データ プロバイダー (<xref:System.Data.SqlClient>、<xref:System.Data.OleDb>) を実行するには、FullTrust アクセス許可が必要です。 アクセス許可レベルが FullTrust より低いゾーンで .NET Framework バージョン 1.0 の .NET Framework データ プロバイダーを使用しようとすると、<xref:System.Security.SecurityException> が発生します。  
  
 ただし、.NET Framework バージョン 2.0 以降では、部分的に信頼されたゾーンですべての .NET Framework データ プロバイダーを使用できるようになりました。 さらに、.NET Framework バージョン 1.1 の .NET Framework データ プロバイダーには、新しいセキュリティ機能が追加されました。 この機能により、特定のセキュリティ ゾーンで使用できる接続文字列を制限することができます。 特定のセキュリティ ゾーンに対して空白のパスワードの使用を禁止することもできます。 詳細については、「 [Code Access Security and ADO.NET](code-access-security.md)」を参照してください。  
  
 .NET Framework のインストールごとに個別の Security.config ファイルがあるため、セキュリティ設定については、互換性の問題はありません。 ただし、アプリケーションが、.NET Framework バージョン 1.1 以降に含まれる ADO.NET の追加のセキュリティ機能に依存している場合は、アプリケーションをバージョン 1.0 のシステムに配布することはできません。  
  
## <a name="sqlcommand-execution"></a>SqlCommand の実行  
 .NET Framework バージョン 1.1 以降では、<xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> によるデータ ソースでのコマンドの実行方法が変更されました。  
  
 .NET Framework バージョン 1.0 の <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> では、すべてのコマンドが **sp_executesql** ストアド プロシージャのコンテキストで実行されました。 その結果、接続の状態に影響を与えるコマンド (たとえば、SET NOCOUNT ON) は、現在のコマンドの実行だけに適用されます。 接続が開かれている間に実行される後続のコマンドについては、接続の状態は変更されません。  
  
 .NET Framework バージョン 1.1 以降の <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> では、コマンドにパラメーターが含まれている場合にのみ、コマンドは **sp_executesql** ストアド プロシージャのコンテキストで実行されます。これにより、パフォーマンスが向上します。 その結果、接続の状態に影響を与えるコマンドが、非パラメーター化コマンドに含まれている場合、接続が開いている間に実行される後続のすべてのコマンドに対して、接続の状態を変更します。  
  
 たとえば、<xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> への呼び出しで次のバッチ コマンドが実行されるとします。  
  
```sql
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
```  
  
 .NET Framework バージョン 1.1 以降では、接続が開かれている間に実行される後続のすべてのコマンドに対して、NOCOUNT は ON のままになります。 .NET Framework バージョン 1.0 では、NOCOUNT は現在のコマンドの実行に対してだけ ON です。  
  
 アプリケーションが、いずれかのバージョンの .NET Framework の <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> の動作に依存している場合、この変更が上位互換性と下位互換性の両方に影響することがあります。  
  
 アプリケーションが新旧両方のバージョンの .NET Framework で実行する場合は、どのバージョンで実行された場合にも動作が同じになるように、コードを記述できます。 変更された接続状態が後続のすべてのコマンドでも有効になるようにする場合は、<xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> を使用してコマンドを実行することをお勧めします。 変更された接続状態が後続のコマンドでは無効になるようにする場合は、接続状態をリセットするコマンドを含めるようにしてください。 次に例を示します。  
  
```sql
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
SET NOCOUNT OFF;  
```  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](ado-net-overview.md)
- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
