---
title: .NET Framework クライアント アプリケーションの作成 (WCF Data Services クイック スタート)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 41ade767-eeab-437d-9121-9797e8fb8045
ms.openlocfilehash: 4beaba24e42b15ebc45ece6e5319a2b14df54ab6
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73975381"
---
# <a name="creating-the-net-framework-client-application-wcf-data-services-quickstart"></a>.NET Framework クライアント アプリケーションの作成 (WCF Data Services クイック スタート)

これは、WCF Data Services クイックスタートの最後のタスクです。 このタスクでは、コンソール アプリケーションをソリューションに追加し、この新しいクライアント アプリケーションに Open Data Protocol (OData) フィードへの参照を追加します。次に、生成されたクライアント データ サービス クラスおよびクライアント ライブラリを使用して、クライアント アプリケーションから OData フィードにアクセスします。

> [!NOTE]
> データ フィードへのアクセスには .NET Framework ベースのクライアント アプリケーションは必要ありません。 データ サービスは、OData フィードを使用する任意のアプリケーション コンポーネントからアクセスできます。 詳細については、「[クライアント アプリケーションでのデータ サービスの使用](using-a-data-service-in-a-client-application-wcf-data-services.md)」を参照してください。

## <a name="to-create-the-client-application-by-using-visual-studio"></a>Visual Studio を使用してクライアント アプリケーションを作成するには

1. **ソリューション エクスプローラー**で該当ソリューションを右クリックして **[追加]** をクリックし、 **[新しいプロジェクト]** をクリックします。

2. 左側のペインで、 **[インストール済み]** > **[Visual C#]** または **[Visual Basic]** > **[Windows デスクトップ]** を選択し、 **[WPF アプリ]** テンプレートを選択します。

3. プロジェクト名に「`NorthwindClient`」と入力し、 **[OK]** をクリックします。

4. ファイル MainWindow.xaml を開き、XAML コードを次のコードに置き換えます。

     [!code-xaml[Astoria Quickstart Client#Window1Xaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml#window1xaml)]

## <a name="to-add-a-data-service-reference-to-the-project"></a>データ サービス参照をプロジェクトに追加するには

1. **ソリューション エクスプローラー**で、NorthwindClient プロジェクトを右クリックして、 **[追加]**  >  **[サービス参照の追加]** をクリックし、 **[探索]** をクリックします。

     最初のタスクで作成した Northwind データ サービスが表示されます。

2. **[名前空間]** テキスト ボックスに「`Northwind`」と入力して、 **[OK]** をクリックします。

     プロジェクトに新しいコード ファイルが追加されます。このコード ファイルには、データ サービス リソースにアクセスし、オブジェクトとしてデータ サービス リソースと対話するデータ クラスが含まれています。 データ クラスは、名前空間 `NorthwindClient.Northwind` で作成されます。

## <a name="to-access-data-service-data-in-the-wpf-application"></a>WPF アプリケーションのデータ サービスにアクセスするには

1. **NorthwindClient** の下の**ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスで、 **[.NET]** タブをクリックし、System.Data.Services.Client.dll アセンブリを選択して、 **[OK]** をクリックします。

3. **NorthwindClient** の下の**ソリューション エクスプローラー**で、MainWindow.xaml ファイルのコード ページを開き、次の `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。

    [!code-csharp[Astoria Quickstart Client#Using](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#using)]
    [!code-vb[Astoria Quickstart Client#Using](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#using)]

4. 次のコードを挿入します。このコードは、データ サービスをクエリし、<xref:System.Data.Services.Client.DataServiceCollection%601> に対する結果を `MainWindow` クラスにバインドします。

    > [!NOTE]
    > ホスト名 `localhost:12345` を Northwind データ サービスのインスタンスをホストするサーバーとポートで置き換えます。

     [!code-csharp[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#querycode)]
     [!code-vb[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#querycode)]

5. 次のコードを挿入します。このコードは、変更内容を `MainWindow` クラスに保存します。

     [!code-csharp[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#savechanges)]
     [!code-vb[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#savechanges)]

## <a name="to-build-and-run-the-northwindclient-application"></a>NorthwindClient アプリケーションをビルドして実行するには

1. **ソリューション エクスプローラー**で NorthwindClient プロジェクトを右クリックして **[スタートアップ プロジェクトに設定]** を選択します。

2. **F5** キーを押してアプリケーションを起動します。

     ソリューションがビルドされ、クライアント アプリケーションが起動します。 データがサービスから要求され、コンソールに表示されます。

3. データ グリッドの **Quantity** 列の値を編集し、 **[保存]** をクリックします。

     変更内容はデータ サービスに保存されます。

    > [!NOTE]
    > このバージョンの NorthwindClient アプリケーションでは、エンティティの追加と削除はサポートされません。

## <a name="next-steps"></a>次の手順

ここでは、サンプル Northwind の OData フィードにアクセスするクライアント アプリケーションを作成しました。 これで WCF Data Services クイックスタートは完了しました。

.NET Framework アプリケーションから OData フィードへのアクセスの詳細については、「[WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [はじめに](getting-started-with-wcf-data-services.md)
- [リソース](wcf-data-services-resources.md)
