---
title: ルーティング サービスを使用した Hello World
ms.date: 03/30/2017
ms.assetid: 0f4b0d5b-6522-4ad5-9f3a-baa78316d7d1
ms.openlocfilehash: 86a2981e8b861da9d5ccf0a34fe037f3ef419aab
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183632"
---
# <a name="hello-world-with-the-routing-service"></a>ルーティング サービスを使用した Hello World
このサンプルでは、Windows 通信基盤 (WCF) ルーティング サービスを示します。 ルーティング サービスは、アプリケーションにコンテンツ ベースのルーターを簡単に含める WCF コンポーネントです。 このサンプルでは、標準の WCF 計算サンプルを、ルーティング サービスを使用して通信するように調整します。 このサンプルの電卓クライアントは、ルーターによって公開されるエンドポイントにメッセージを送信するように構成されています。 ルーティング サービスは、送信されてきたすべてのメッセージを受け入れ、電卓サービスに対応するエンドポイントに転送するように構成されています。 したがって、クライアントから送信されたメッセージはルーターで受信され、実際の電卓サービスに再ルーティングされます。 電卓サービスからのメッセージはルーターに送り返され、ルーターから電卓クライアントに渡されます。

### <a name="to-use-this-sample"></a>このサンプルを使用するには

1. ビジュアル スタジオ 2012 を使用して、を開きます。

2. F5 キーを押すか、Ctrl キーと Shift キーを押しながら B キーを押します。

    > [!NOTE]
    > F5 キーを押した場合は、電卓クライアントが自動的に起動します。 Ctrl キーと Shift キーを押しながら B キーを押した (ビルドする) 場合は、次のアプリケーションを手動で開始する必要があります。
    >
    > 1. 電卓クライアント (./CalculatorClient/bin/client.exe)
    > 2. 電卓サービス (./CalculatorService/bin/service.exe)
    > 3. ルーティング サービス (./RoutingService/bin/RoutingService.exe)

3. Enter キーを押してクライアントを起動します。

     次の出力が表示されます。

    ```console
     Add(100,15.99) = 115.99

     Subtract(145,76.54) = 68.46

     Multiply(9,81.25) = 731.25

     Divide(22,7) = 3.14285714285714
    ```

## <a name="configurable-via-code-or-appconfig"></a>コードまたは App.Config で構成可能
 サンプルは、提供された時点では、App.config ファイルを使用してルーターの動作を定義するように構成されています。 App.config ファイルの名前を別の名前に変更して認識されないようにし、ConfigureRouterViaCode() に対するメソッド呼び出しのコメントを解除することもできます。 どちらの方法でも、ルーターの動作は同じになります。

### <a name="scenario"></a>シナリオ
 このサンプルでは、基本的なメッセージ ポンプとして機能するルーターを示します。 ルーティング サービスは、構成済みの一連の送信先エンドポイントに直接メッセージを渡すように構成された透過的なプロキシ ノードとして機能します。

### <a name="real-world-scenario"></a>実際のシナリオ
 Contoso では、サービスの名前指定、アドレス指定、構成、およびセキュリティに関する柔軟性を高めるために、 基本的なメッセージ ポンプをサービスの前に配置して、それをエンドポイントとして公開しています。 これにより、実際のサービスの前にセキュリティが追加され、スケールアウトされたソリューションやサービスのバージョン管理を後で簡単に実装できるようになります。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\RoutingServices\HelloRoutingService`  
  
## <a name="see-also"></a>関連項目

- [AppFabric のホストおよび永続化のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
