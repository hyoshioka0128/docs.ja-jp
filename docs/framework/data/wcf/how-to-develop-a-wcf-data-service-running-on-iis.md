---
title: '方法: IIS 上で実行する WCF Data Service を開発する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- WCF Data Services, hosting
ms.assetid: f6f768c5-4989-49e3-a36f-896ab4ded86e
ms.openlocfilehash: 8a1a0c2c55267940463e2c9ab82bb52345269260
ms.sourcegitcommit: 43cbde34970f5f38f30c43cd63b9c7e2e83717ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81121610"
---
# <a name="how-to-develop-a-wcf-data-service-running-on-iis"></a>方法: IIS 上で実行する WCF Data Service を開発する

この記事では、WCF Data Services を使用して、Northwind サンプル データベースに基づいてデータ サービスを作成する方法を示します。このサンプル データベースは、インターネット インフォメーション サービス (IIS) 上で実行されている ASP.NET Web アプリによってホストされます。 同じ Northwind データ サービスを ASP.NET 開発サーバーで実行する ASP.NET Web アプリとして作成する方法の例については、[WCF Data Services のクイックスタート](quickstart-wcf-data-services.md)を参照してください。

> [!NOTE]
> Northwind データ サービスを作成するには、まず、ローカル コンピューターに Northwind サンプル データベースをインストールします。 データベースをインストールするには、[Microsoft SQL Serverの Northwind および pubs サンプル データベース](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)から Transact-SQL スクリプトを実行します。

この記事では、Entity Framework プロバイダーを使用してデータ サービスを作成する方法を示します。 その他のデータ サービス プロバイダーを利用することもできます。 詳細については、「[Data Services プロバイダー](data-services-providers-wcf-data-services.md)」を参照してください。

サービスを作成した後に、データ サービス リソースへのアクセスを明示的に提供する必要があります。 詳細については、[データ サービスへのアクセスを有効にする](how-to-enable-access-to-the-data-service-wcf-data-services.md)」を参照してください。

## <a name="create-the-aspnet-web-application-that-runs-on-iis"></a>IIS 上で実行する ASP.NET Web アプリケーションを作成する

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[インストール済み]** > [**Visual C#** または **Visual Basic**] > **[Web]** カテゴリを選択します。

3. **[ASP.NET Web アプリケーション]** テンプレートを選択します。

4. プロジェクトの名前として「`NorthwindService`」を入力します。

5. **[OK]** をクリックします。

6. **[プロジェクト]** メニューで **[NorthwindService のプロパティ]** を選択します。

7. **[Web]** タブで **[ローカル IIS Web サーバーを使用する]** を選択します。

8. **[仮想ディレクトリの作成]** 、 **[OK]** の順にクリックします。

9. 管理特権を持つコマンド プロンプトから、次のコマンドを実行します (オペレーティング システムによって異なります)。

    - 32 ビット システム:

        ```console
        "%windir%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

    - 64 ビット システム:

        ```console
        "%windir%\Microsoft.NET\Framework64\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

     これにより、コンピューターに Windows Communication Foundation (WCF) が登録されます。

10. 管理特権を持つコマンド プロンプトから、次のコマンドを実行します (オペレーティング システムによって異なります)。

    - 32 ビット システム:

        ```console
        "%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

    - 64 ビット システム:

        ```console
        "%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

     これにより、WCF がコンピューターにインストールされた後、IIS は正常に実行されます。 IIS の再起動が必要になる場合があります。

11. ASP.NET アプリケーションが IIS7 で実行されると、次の手順も実行する必要があります。

    1. IIS マネージャーを開いて **[既定の Web サイト]** の下にある PhotoService アプリケーションに移動します。

    2. **[機能ビュー]** で、 **[認証]** をダブルクリックします。

    3. **[認証]** ページで、 **[匿名認証]** を選択します。

    4. **[操作]** ペインで **[編集]** をクリックして、匿名ユーザーがサイトに接続するときのセキュリティ プリンシパルを設定します。

    5. **[匿名認証資格情報の編集]** ダイアログ ボックスで、 **[アプリケーション プール ID]** をクリックします。

    > [!IMPORTANT]
    > ネットワーク サービス アカウントを使用する際、そのアカウントに関連するすべての内部ネットワーク アクセス権を匿名ユーザーに付与します。

12. SQL Server Management Studio、sqlcmd.exe ユーティリティ、または Visual Studio の Transact-SQL エディターを使用して、Northwind データベースがアタッチされた SQL Server のインスタンスに対して次の Transact-SQL コマンドを実行します。

    ```sql
    CREATE LOGIN [NT AUTHORITY\NETWORK SERVICE] FROM WINDOWS;
    GO
    ```

    これにより、IIS の実行に使用される Windows アカウントに対して、SQL Server インスタンスのログインが作成されます。 IIS は、これを使用して SQL Server インスタンスに接続できるようになります。

13. Northwind データベースをアタッチして、次の Transact-SQL コマンドを実行します。

    ```sql
    USE Northwind
    GO
    CREATE USER [NT AUTHORITY\NETWORK SERVICE]
    FOR LOGIN [NT AUTHORITY\NETWORK SERVICE] WITH DEFAULT_SCHEMA=[dbo];
    GO
    ALTER LOGIN [NT AUTHORITY\NETWORK SERVICE]
    WITH DEFAULT_DATABASE=[Northwind];
    GO
    EXEC sp_addrolemember 'db_datareader', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    EXEC sp_addrolemember 'db_datawriter', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    ```

    これにより、新しいログインに権限が付与され、IIS は Northwind データベースに対してデータの読み取りおよび書き込みを行うことができるようになります。

## <a name="define-the-data-model"></a>データ モデルを定義する

1. **ソリューション エクスプローラー**で、ASP.NET プロジェクトの名前を右クリックし、 **[追加]**  >  **[新しい項目]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで **[ADO.NET エンティティ データ モデル]** を選択します。

3. データ モデルの名前として「`Northwind.edmx`」を入力します。

4. Entity Data Model ウィザードで **[データベースから生成する]** を選択し、 **[次へ]** をクリックします。

5. 次のいずれかの手順を実行してデータ モデルをデータベースに接続してから **[次へ]** をクリックします。

    - データベース接続がまだ構成されていない場合は、 **[新しい接続]** をクリックして新しい接続を作成します。 詳細については、[SQL Server データベースへの接続を作成する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/s4yys16a(v=vs.90))」を参照してください。 この SQL Server インスタンスには、Northwind サンプル データベースがアタッチされている必要があります。

         \- または

    - Northwind データベースに接続するようにデータベース接続が既に構成されている場合は、一覧からその接続を選択します。

6. ウィザードの最終ページで、データベース内のすべてのテーブルのチェック ボックスをオンにし、ビューおよびストアド プロシージャのチェック ボックスをオフにします。

7. **[完了]** をクリックして、ウィザードを終了します。

## <a name="create-the-data-service"></a>データ サービスを作成する

1. **ソリューション エクスプローラー**で、ASP.NET プロジェクトの名前を右クリックし、 **[追加]**  >  **[新しい項目]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[WCF Data Service]** をクリックします。

   ![Visual Studio 2015 の WCF Data Service 項目テンプレート](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF Data Service** テンプレートは Visual Studio 2015 で使用できますが、Visual Studio 2017 以降では使用できません。

3. サービスの名前として、「`Northwind`」と入力します。

     Visual Studio で新しいサービスの XML マークアップおよびコード ファイルが作成されます。 既定では、コード エディターのウィンドウが開きます。 **ソリューション エクスプローラー**では、このサービスに Northwind という名前が付き、拡張子は .svc.cs または .svc.vb になります。

4. データ サービスのコードで、データ サービスを定義するクラスの定義にあるコメント `/* TODO: put your data source class name here */` をデータ モデルのエンティティ コンテナーである型 (この場合は `NorthwindEntities`) で置き換えます。 クラス定義は次のようになります。

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

## <a name="see-also"></a>関連項目

- [サービスとしてのデータの公開](exposing-your-data-as-a-service-wcf-data-services.md)
