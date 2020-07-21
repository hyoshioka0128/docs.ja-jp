---
title: SQL 追跡
ms.date: 03/30/2017
ms.assetid: bcaebeb1-b9e5-49e8-881b-e49af66fd341
ms.openlocfilehash: 72bfcaac2903b3e7fa5679422ad4feaa79e93211
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81243181"
---
# <a name="sql-tracking"></a>SQL トラッキング

このサンプルでは、追跡レコードを SQL データベースに書き込むカスタム SQL 追跡参加要素を記述する方法を示します。 Windows ワークフロー基盤 (WF) では、ワークフロー インスタンスの実行を可視化するためのワークフロー追跡機能が提供されます。 追跡ランタイムでは、ワークフローの実行中にワークフロー追跡レコードが出力されます。 ワークフロー追跡の詳細については、「[ワークフローの追跡とトレース](../workflow-tracking-and-tracing.md)」を参照してください。

## <a name="use-the-sample"></a>サンプルを使用する

1. SQL Server 2008、SQL Server 2008 Express、またはそれ以降のバージョンがインストールされていることを確認します。 サンプルと共にパッケージ化されているスクリプトは、SQL Express インスタンスをローカル コンピューターで使用していることが前提になります。 別のインスタンスがある場合は、データベース関連のスクリプトを変更してからサンプルを実行してください。

2. Scripts ディレクトリ (\WF\Basic\Tracking\SqlTracking\CS\Scripts) 内で Trackingsetup.cmd を実行して SQL Server 追跡データベースを作成します。 これによって、TrackingSample という名前のデータベースが作成されます。

   > [!NOTE]
   > このスクリプトでは、SQL Express の既定のインスタンスにデータベースが作成されます。 別のデータベース インスタンスにインストールする場合は、Trackingsetup.cmd スクリプトを編集してください。

3. 2010 で SqlTrackingSample.sln を開きます。

4. **Ctrl**+**Shift**+**B**キーを押してソリューションをビルドします。

5. **F5** キーを押してアプリケーションを実行します。

   ブラウザー ウィンドウが開き、アプリケーションのディレクトリの一覧が示されます。

6. ブラウザーで、StockPriceService.xamlx をクリックします。

7. ブラウザーに、[StockPriceService] ページが表示され、ローカル サービスの WSDL アドレスが示されます。 このアドレスをコピーします。

   ローカル サービスの WSDL アドレスの`http://localhost:65193/StockPriceService.xamlx?wsdl`例は です。

8. ファイル エクスプローラーを使用して、WCF テスト クライアント (WcfTestClient.exe) を実行します。 これは *、Microsoft Visual Studio 10.0\Common7\IDE ディレクトリ*にあります。

9. WCF テスト クライアントで、[**ファイル**] メニューをクリックし、[**サービスの追加**] を選択します。 テキスト ボックスにローカル サービスのアドレスを貼り付けます。 [**OK**] をクリックしてダイアログ ボックスを閉じます。

10. WCF テスト クライアントで、[**価格の取得**] をダブルクリックします。 1 つの`GetStockPrice`パラメータを受け取る操作が開き`Contoso`、値を入力して **[Invoke]** をクリックします。

11. 出力された追跡レコードが SQL データベースに書き込まれます。 追跡レコードを表示するには、SQL Management Studio で TrackingSample データベースを開き、テーブルに移動します。 テーブルで選択クエリを実行すると、それぞれのテーブルに格納されている追跡レコード内のデータが表示されます。

   SQL Server 管理スタジオの詳細については、「 [SQL Server 管理スタジオの概要](/sql/ssms/sql-server-management-studio-ssms)」を参照してください。 SQL Server 管理スタジオを[ダウンロード](https://aka.ms/ssmsfullsetup)します。

## <a name="uninstall-the-sample"></a>サンプルをアンインストールする

1. サンプル ディレクトリ (*\WF\基本\追跡\SqlTracking)* で追跡クリーンアップ.cmd スクリプトを実行します。

    > [!NOTE]
    > Trackingcleanup.cmd は、ローカル コンピューターの SQL Express 内にあるデータベースを削除しようとします。 別の SQL Server インスタンスを使用している場合は、Trackingcleanup.cmd を編集します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\SqlTracking`

## <a name="see-also"></a>関連項目

- [AppFabric の監視のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))
