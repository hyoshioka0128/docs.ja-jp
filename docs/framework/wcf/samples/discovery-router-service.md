---
title: 探索ルーター サービス
ms.date: 03/30/2017
ms.assetid: 3d30af47-b24f-40e5-833a-24d77125c9e6
ms.openlocfilehash: 149dd69cdd1972465f4b7cb48ab657492d3f21d7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183729"
---
# <a name="discovery-router-service"></a>探索ルーター サービス
このサンプルでは、探索メッセージを別のエンドポイントに転送する方法を示します。  
  
## <a name="demonstrates"></a>対象  
 探索ルーティング  
  
## <a name="discussion"></a>ディスカッション  
 探索ルーティングは、プロキシがサービスを認識しないが、別のプロキシのことは認識する場合に、クライアントがプロキシを使用してそのようなサービスを検索するシナリオで役に立ちます。 このプロキシは、探索パケットをこのクライアントから 2 番目のプロキシに転送できます。 2 番目のプロキシはサービスを検索し、応答を元のクライアントに返します。  
  
 このサンプルでは、クライアントはメッセージを探索ルーティング コンポーネントに送信します。 このメッセージは、探索ルーター上の特定のエンドポイントに送信されます。 その後、このルーターはメッセージを UDP マルチキャスト エンドポイントに転送します。 プローブ メッセージはマルチキャスト エンドポイントに送信され、UDP マルチキャスト アドレスをリッスンするサービスは、その探索ルーターに応答します。 探索ルーターは応答を収集し、クライアントにその応答を返します。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. サンプルをビルドします。  
  
2. DiscoveryRouter 実行可能ファイルを実行します。  
  
3. ビルド ディレクトリからサービス実行可能ファイルを実行します。  
  
4. クライアント実行可能ファイルを実行します。 クライアントでサービスが検索されることに注意してください。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryRouter`
