---
title: SqlClient による LocalDB のサポート
ms.date: 03/30/2017
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.openlocfilehash: d02524cd5901adeca7bc36d6fd13c7abdc46c69b
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894403"
---
# <a name="sqlclient-support-for-localdb"></a>SqlClient による LocalDB のサポート
SQL Server コード名 Denali 以降、SQL Server の簡易バージョンである LocalDB を使用できるようになります。 ここでは、LocalDB データベースに接続する方法について説明します。  
  
## <a name="remarks"></a>Remarks  
 LocalDB のインストール方法や LocalDB インスタンスの構成方法など、LocalDB の詳細については、SQL Server オンライン ブックを参照してください。  
  
 LocalDB で実行できる操作の概要を次に示します。  
  
- sqllocaldb.exe または app.config ファイルを使用して LocalDB インスタンスを作成および開始する。  
  
- sqlcmd.exe を使用して LocalDB インスタンスにデータベースを追加および変更する。 たとえば、 `sqlcmd -S (localdb)\myinst`のようにします。  
  
- `AttachDBFilename` 接続文字列キーワードを使用して LocalDB インスタンスにデータベースを追加する。 `AttachDBFilename`を使用していて、 `Database` 接続文字列キーワードでデータベースの名前を指定しない場合、アプリケーションを閉じると、データベースは LocalDB インスタンスから削除されます。  
  
- 接続文字列に LocalDB インスタンスを指定する。 たとえば、インスタンス名が `myInstance`の場合、接続文字列には次の行が含まれます。  
  
    `server=(localdb)\\myInstance`  
  
 `User Instance=True` は LocalDB データベースに接続するときに使用することはできません。  
  
 LocalDB は [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=29065)からダウンロードできます。 sqlcmd.exe を使用し、LocalDB インスタンスのデータを変更する場合、SQL Server 2012 の sqlcmd が表になります。これは SQL Server 2012 Feature Pack からも入手できます。  
  
## <a name="programmatically-create-a-named-instance"></a>名前付きインスタンスをプログラムによって作成する  
 アプリケーションは、次のように名前付きインスタンスを作成してデータベースを指定できます。  
  
- app.config ファイルに作成するための LocalDB インスタンスを次のように指定する。  インスタンスのバージョン番号は LocalDB インストールのバージョン番号と同じである必要があります。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- `server` 接続文字列キーワードを使用してインスタンス名を指定する。  `server` 接続文字列キーワードで指定されたインスタンス名は app.config ファイルで指定された名前と一致する必要があります。  
  
- .MDF ファイルを指定するには、 `AttachDBFilename` 接続文字列キーワードを使用する。  
  
## <a name="see-also"></a>関連項目

- [SQL Server の機能と ADO.NET](sql-server-features-and-adonet.md)
- [ADO.NET の概要](../ado-net-overview.md)
