---
title: LINQ メッセージ クエリの関連付け
ms.date: 03/30/2017
ms.assetid: b746872e-57b1-4514-b337-53398a0e0deb
ms.openlocfilehash: 507001b165efdcbe7c1e27a07749dbe2eafb468f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182803"
---
# <a name="linq-message-query-correlation"></a>LINQ メッセージ クエリの関連付け
このサンプルでは、システム標準の <xref:System.ServiceModel.Dispatcher.MessageQuery> ではなく、カスタムの <xref:System.ServiceModel.XPathMessageQuery> 実装を使用して、コンテンツ ベースの関連付けを実行する方法を示します。  
  
## <a name="demonstrates"></a>対象  
 カスタムの <xref:System.ServiceModel.Dispatcher.MessageQuery>、コンテンツ ベースの相関関係。  
  
## <a name="discussion"></a>ディスカッション  
 このサンプルでは、関連付けのために <xref:System.ServiceModel.Dispatcher.MessageQuery> 基本クラスから拡張する方法を示します。 カスタム実装の `LinqMessageQuery` を使用すると、XLinq を使用してメッセージ内で検索する XName を指定できます。 クエリによって取得されたデータを使用して、メッセージを適切なワークフロー インスタンスにディスパッチするための相関関係キーを作成します。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. このサンプルでは、HTTP エンドポイントを使用してワークフロー サービスを公開します。 このサンプルを実行するには、Visual Studio を管理者として実行するか、管理者特権のプロンプトで次のコマンドを実行して適切な ACL を追加する (詳細については[、HTTP および HTTPS](../../wcf/feature-details/configuring-http-and-https.md)の構成を参照) 必要があります。 ドメインとユーザー名は置き換えてください。  
  
    ```console  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2. URL ACL を追加したら、次の手順を実行します。  
  
    1. ソリューションをビルドします。  
  
    2. ソリューションを右クリックし、[スタートアップ プロジェクトの設定] を選択して、複数の**スタートアップ プロジェクトを設定**します。 **サービス**と**クライアント**を複数のスタートアップ プロジェクトとして (この順序で) 追加します。  
  
    3. アプリケーションを実行します。 クライアント コンソールには、注文を送信し、発注書 ID を受信した後に、注文を確認するワークフローが示されます。 Service のウィンドウには、処理されている要求が示されます。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\LinqMessageQueryCorrelation`
