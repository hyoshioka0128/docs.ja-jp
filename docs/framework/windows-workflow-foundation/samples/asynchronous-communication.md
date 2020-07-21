---
title: 非同期通信
ms.date: 03/30/2017
ms.assetid: 128dc092-9eb2-4e33-9470-9a7f62b60df6
ms.openlocfilehash: e1bc63b5d3178b8e98350dedd8eb0791e0e35589
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142877"
---
# <a name="asynchronous-communication"></a>非同期通信
このサンプルでは、2 つの異なる Windows ワークフローファンデーション (WF) サービス間の通信が既定で非同期的に行われる方法を示します。  
  
## <a name="demonstrates"></a>対象  
 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] サービス間の非同期通信  
  
## <a name="discussion"></a>ディスカッション  
 このサンプルでは、.NET Framework が提供するメッセージング アクティビティを使用して、[!INCLUDE[wf1](../../../../includes/wf1-md.md)] アプリケーション間の非同期通信がどのように行われるのかを示します。  
  
 このサンプルは、次の 3 つのプロジェクトで構成されています。  
  
 CreditCheckService  
 このサービスは、特定の個人のクレジット スコアまたは取得する項目の値を受け取り、その個人にクレジットを与えるかどうかを判断します。  
  
 RentalApprovalService  
 このサービスは、特定のクレジットを必要としている個人から申請を受け取ります。 このサービスは `CreditCheckService` と非同期で通信して、クレジットの申請が有効かどうかを判断します。  
  
 Client  
 クライアントは `RentalApprovalService` と同期通信を行い、クレジットが承認されているかどうかを調べます。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. **非同期通信**ソリューションを右クリックし、[**プロパティ ]** を選択します。  
  
2. [**共通プロパティ]** で [**スタートアップ プロジェクト**] を選択し、[**複数のスタートアップ プロジェクト**] を選択します。  
  
3. リストの最初の位置に**レンタル承認サービス**を移動し、次に**CreditCheckService**を移動し、次に**クライアントを移動します**。 3 つのプロジェクトすべてに対して**開始**アクションを設定します。  
  
4. **[OK]** をクリックし、F5 キーを押してサンプルを実行します。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\AsynchronousCommunication`
