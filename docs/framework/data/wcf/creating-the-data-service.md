---
title: Visual Studio で WCF のデータ サービスを作成する
description: WCF Data Services を使用するサンプル データ サービスを作成し、サンプル データベースに基づいて OData フィードを公開する方法について説明します。
ms.date: 08/24/2018
dev_langs:
- csharp
- vb
ms.assetid: 34d1d971-5e18-4c22-9bf6-d3612e27ea59
ms.openlocfilehash: 739cb6971209792724a2e939ca4f4821d5879c8c
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247792"
---
# <a name="create-the-data-service"></a>データ サービスを作成する

このトピックでは、WCF Data Services を使用して、Northwind サンプル データベースに基づく Open Data Protocol (OData) フィードを公開するサンプル データ サービスを作成します。 この作業に必要な基本手順は次のとおりです。

1. ASP.NET Web アプリケーションを作成します。

2. Entity Data Model ツールを使用して、データ モデルを定義します。

3. データ サービスを Web アプリケーションに追加します。

4. データ サービスへのアクセスを有効にします。

## <a name="create-the-aspnet-web-app"></a>ASP.NET Web アプリを作成する

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

1. **[新しいプロジェクト]** ダイアログ ボックスで、Visual Basic または Visual C# の **[Web]** カテゴリを選択し、 **[ASP.NET Web アプリケーション]** を選択します。

1. プロジェクトの名前として「`NorthwindService`」と入力し、 **[OK]** を選択します。

1. **[新しい ASP.NET Web アプリケーション]** ダイアログで、 **[空]** を選択し、 **[OK]** を選択します。

1. (省略可能) Web アプリケーションに対して特定のポート番号を指定します。 注: この一連のクイックスタート トピックでは、ポート番号 `12345` が使用されています。

    1. **ソリューション エクスプローラー**で、作成した ASP.NET プロジェクトを右クリックし、 **[プロパティ]** を選択します。

    2. **[Web]** タブを選択し、 **[ポートを指定する]** ボックスの値を `12345` に設定します。

## <a name="define-the-data-model"></a>データ モデルを定義する

1. **ソリューション エクスプローラー**で、ASP.NET プロジェクトの名前を右クリックし、 **[追加]**  >  **[新しい項目]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで **[データ]** カテゴリを選択し、 **[ADO.NET Entity Data Model]** を選択します。

3. データ モデルの名前として「`Northwind.edmx`」と入力します。

4. **Entity Data Model ウィザード**で **[データベースの EF デザイナー]** を選択し、 **[次へ]** をクリックします。

5. 次のいずれかの手順を実行してデータ モデルをデータベースに接続してから **[次へ]** をクリックします。

    - データベース接続がまだ構成されていない場合は、 **[新しい接続]** をクリックして新しい接続を作成します。 詳細については、「[方法:SQL Server データベースへの接続を作成する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/s4yys16a(v=vs.90))」を参照してください。 この SQL Server インスタンスには、Northwind サンプル データベースがアタッチされている必要があります。

         \- または

    - Northwind データベースに接続するようにデータベース接続が既に構成されている場合は、一覧からその接続を選択します。

6. ウィザードの最終ページで、データベース内のすべてのテーブルのチェック ボックスをオンにし、ビューおよびストアド プロシージャのチェック ボックスをオフにします。

7. **[完了]** をクリックして、ウィザードを終了します。

## <a name="create-the-wcf-data-service"></a>WCF データ サービスを作成する

1. **ソリューション エクスプローラー**で、ASP.NET プロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[Web]** カテゴリの **[WCF Data Service]** 項目テンプレートを選択します。

   ![Visual Studio 2015 の WCF Data Service 項目テンプレート](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF Data Service** テンプレートは Visual Studio 2015 で使用できますが、Visual Studio 2017 以降では使用できません。

3. サービスの名前として、「`Northwind`」と入力します。

     Visual Studio で新しいサービスの XML マークアップおよびコード ファイルが作成されます。 既定では、コード エディターのウィンドウが開きます。 **ソリューション エクスプローラー**では、このサービスに Northwind という名前が付き、拡張子は *.svc.cs* または *.svc.vb* になります。

4. データ サービスのコードで、データ サービスを定義するクラスの定義にあるコメント `/* TODO: put your data source class name here */` をデータ モデルのエンティティ コンテナーである型 (この場合は `NorthwindEntities`) で置き換えます。 クラス定義は次のようになります。

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

## <a name="enable-access-to-data-service-resources"></a>データ サービス リソースへのアクセスを有効にする

1. データ サービスのコードで、`InitializeService` 関数のプレースホルダーのコードを次の内容で置き換えます。

     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#allreadconfig)]

     これにより、承認されたクライアントは、指定したエンティティ セットのリソースに読み取りおよび書き込みアクセスできるようになります。

    > [!NOTE]
    > ASP.NET アプリケーションにアクセスできるクライアントは、データ サービスによって公開されるリソースにもアクセスできます。 運用データ サービスで、リソースへの承認されていないアクセスを防止するために、アプリケーション自身もセキュリティで保護する必要があります。 詳細については、「 [Securing WCF Data Services](securing-wcf-data-services.md)」を参照してください。

## <a name="next-steps"></a>次の手順

ここでは、Northwind サンプル データベースに基づいて、OData フィードを公開する新しいデータ サービスを作成し、ASP.NET Web アプリケーションへのアクセス許可を持つクライアントからフィードへのアクセスを有効にしました。 次は、Visual Studio からデータ サービスを開始して、Web ブラウザーから HTTP GET 要求を送信して OData フィードにアクセスします。

> [!div class="nextstepaction"]
> [Web ブラウザーからサービスにアクセスする](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

## <a name="see-also"></a>関連項目

- [ADO.NET Entity Data Model ツール](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
