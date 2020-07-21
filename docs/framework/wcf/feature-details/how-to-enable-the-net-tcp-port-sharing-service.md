---
title: '方法: Net.TCP ポート共有サービスを有効にする'
description: Net.tcp を有効にするために、MMC を使用して Net TCP ポート共有サービスを構成する方法について説明します。 Net.tcp は、既定で無効になっています。
ms.date: 03/30/2017
helpviewer_keywords:
- port sharing [WCF]
- activation services [WCF]
ms.assetid: c9175af4-c27c-4765-bf45-b8f7528a7282
ms.openlocfilehash: 0292559e3befde7f0b00b36aa10a2d9615daf049
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247001"
---
# <a name="how-to-enable-the-nettcp-port-sharing-service"></a>方法: Net.TCP ポート共有サービスを有効にする
Windows Communication Foundation (WCF) は、Net.tcp ポート共有サービスと呼ばれる Windows サービスを使用して、複数のプロセスで TCP ポートを共有しやすくします。 このサービスは WCF の一部としてインストールされますが、セキュリティ上の理由から、既定ではサービスが有効になっていないため、最初に使用する前に手動で有効にする必要があります。 このトピックでは、Microsoft 管理コンソール (MMC) スナップインを使用して、Net TCP ポート共有サービスを設定する方法について説明します。  
  
 Net.tcp ポート共有サービスを有効にし、手動で開始したら、「[方法: ポート共有を使用するように WCF サービスを構成](how-to-configure-a-wcf-service-to-use-port-sharing.md)する」を参照して、このサービスを使用するようにサービスを構成する方法について説明します。  
  
 Net.tcp://ポート共有を使用するサンプルについては、 [Net.tcp ポート共有のサンプル](../samples/net-tcp-port-sharing-sample.md)を参照してください。  
  
### <a name="to-enable-the-nettcp-port-sharing-service-using-mmc"></a>MMC を使用して Net.TCP ポート共有サービスを有効にするには  
  
1. [スタート] メニューから、[サービス] 管理コンソールを開きます。そのためには、コマンドプロンプトウィンドウを開き、「」と入力 `services.msc` するか、[実行] を開き、[開く] ボックスに「」と入力し `services.msc` ます。  
  
2. サービスの一覧の [**名前**] 列で、 **Net.tcp ポート共有サービス**を右クリックし、メニューから [**プロパティ**] を選択します。  
  
3. サービスの手動起動を有効にするには、[**プロパティ**] ウィンドウで [**全般**] タブを選択し、[**スタートアップの種類**] ボックスで [手動] を選択して、[**適用**] をクリックします。  
  
4. サービスを開始するには、[サービスの状態] 領域で [**開始**] ボタンをクリックします。 これで、サービスの状態には "開始" が表示されます。  
  
5. サービスの一覧に戻るには、[ **OK]** をクリックして、MMC コンソールを終了します。  
  
## <a name="example"></a>例  
  
## <a name="see-also"></a>関連項目

- [Net.TCP ポート共有](net-tcp-port-sharing.md)
- [Net.TCP ポート共有サービスを構成する](configuring-the-net-tcp-port-sharing-service.md)
