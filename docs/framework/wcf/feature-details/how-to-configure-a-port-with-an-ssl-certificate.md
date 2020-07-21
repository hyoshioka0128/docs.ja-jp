---
title: '方法: SSL 証明書を使用してポートを構成する'
description: X.509 証明書を使用してポートを構成する方法について説明します。これは、transport security を使用して、WSHttpBinding クラスの自己ホスト型 WCF サービスに必要です。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SSL
- WCF, security mode
- WCF, security
ms.assetid: b8abcc8e-a5f5-4317-aca5-01e3c40ab24d
ms.openlocfilehash: 0eccdf916dae7b886cbc4e6563e6dfe17039c321
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247183"
---
# <a name="how-to-configure-a-port-with-an-ssl-certificate"></a>方法: SSL 証明書を使用してポートを構成する

トランスポートセキュリティを使用するクラスを使用して自己ホスト型 Windows Communication Foundation (WCF) サービスを作成する場合は、 <xref:System.ServiceModel.WSHttpBinding> x.509 証明書を使用してポートを構成する必要もあります。 自己ホスト型サービスを作成するのでなければ、インターネット インフォメーション サービス (IIS) でサービスをホストできます。 詳細については、「 [HTTP トランスポートセキュリティ](http-transport-security.md)」を参照してください。  
  
 ポートを構成する場合に使用するツールは、コンピューターで実行されているオペレーティング システムによって異なります。  
  
 Windows Server 2003 を実行している場合は、HttpCfg.exe ツールを使用します。 Windows Server 2003 では、このツールはインストールされています。 詳細については、「 [httpcfg.exe の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc787508(v=ws.10))」を参照してください。 [Windows サポートツールのドキュメント](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc781601(v=ws.10))では、Httpcfg.exe ツールの構文について説明しています。  
  
 Windows Vista を実行している場合は、既にインストールされている Netsh.exe ツールを使用します。
  
> [!NOTE]
> コンピューターに保存されている証明書を変更するには、管理者特権が必要です。  
  
## <a name="determine-how-ports-are-configured"></a>ポートの構成方法を決定する  
  
1. Windows Server 2003 または Windows XP では、次の例に示すように、HttpCfg.exe ツールを使用して現在のポート構成を表示します。**クエリ**と**ssl**スイッチを使用します。  
  
    ```console
    httpcfg query ssl  
    ```  
  
2. Windows Vista では、次の例に示すように、Netsh.exe ツールを使用して現在のポート構成を表示します。  
  
    ```console  
    netsh http show sslcert  
    ```  
  
## <a name="get-a-certificates-thumbprint"></a>証明書の拇印を取得する  
  
1. 証明書 MMC スナップインを使用して、クライアント認証を目的として含む X.509 証明書を検索します。 詳細については、「 [方法: MMC スナップインを使用して証明書を参照する](how-to-view-certificates-with-the-mmc-snap-in.md)」をご覧ください。  
  
2. 証明書の拇印にアクセスします。 詳細については、「[方法: 証明書のサムプリントを取得する](how-to-retrieve-the-thumbprint-of-a-certificate.md)」を参照してください。  
  
3. 証明書のサムプリントを、メモ帳などのテキスト エディターにコピーします。  
  
4. 16 進文字の間にある空白をすべて削除します。 たとえばエディターの "すべて置換" 機能を使用して、空白を空文字列に置き換えるとよいでしょう。  
  
## <a name="bind-an-ssl-certificate-to-a-port-number"></a>SSL 証明書をポート番号にバインドする  
  
1. Windows Server 2003 または Windows XP では、Secure Sockets Layer (SSL) ストアの "設定" モードで HttpCfg.exe ツールを使用して、証明書をポート番号にバインドします。 このツールは、次のように、拇印を使用して証明書を識別します。  
  
    ```console  
    httpcfg set ssl -i 0.0.0.0:8012 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6  
    ```  
  
    - **-I**スイッチの構文はです。は、 `IP` `port` コンピューターのポート8012に証明書を設定するようにツールに指示します。 "0.0.0.0" の部分は、必要に応じて、コンピューターの実際の IP アドレスに置き換えてください。  
  
    - **-H**スイッチは、証明書の拇印を指定します。  
  
2. Windows Vista では、次の例に示すように、Netsh.exe ツールを使用します。  
  
    ```console  
    netsh http add sslcert ipport=0.0.0.0:8000 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}
    ```  
  
    - **Certhash**パラメーターは、証明書の拇印を指定します。  
  
    - **Ipport**パラメーターには、IP アドレスとポートを指定します。また、「」で説明されている Httpcfg.exe ツールの **-i**スイッチと同様に機能します。  
  
    - **Appid**パラメーターは、所有しているアプリケーションを識別するために使用できる GUID です。  
  
## <a name="bind-an-ssl-certificate-to-a-port-number-and-support-client-certificates"></a>SSL 証明書をポート番号にバインドし、クライアント証明書をサポートする  
  
1. Windows Server 2003 または Windows XP で、トランスポート層で x.509 証明書を使用して認証を行うクライアントをサポートするには、前の手順に従いますが、次の例に示すように、HttpCfg.exe に追加のコマンドラインパラメーターを渡します。  
  
    ```console  
    httpcfg set ssl -i 0.0.0.0:8012 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6 -f 2  
    ```  
  
     **-F**スイッチには、の構文があり `n` ます。 n は 1 ~ 7 の数値です。 前の例のように 2 を指定すると、クライアントはトランスポート層で認証することになります。 値として 3 を指定すると、クライアント証明書が有効になり、それらの証明書が Windows アカウントに対応付けられます。 他の値については、HttpCfg.exe のヘルプ機能を参照してください。  
  
2. Windows Vista で、トランスポート層で x.509 証明書を使用して認証を行うクライアントをサポートするには、次の例に示すように、上記の手順に従いますが、追加のパラメーターを指定します。  
  
    ```console  
    netsh http add sslcert ipport=0.0.0.0:8000 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF} clientcertnegotiation=enable  
    ```  
  
## <a name="delete-an-ssl-certificate-from-a-port-number"></a>ポート番号から SSL 証明書を削除する  
  
1. HttpCfg.exe または Netsh.exe ツールを使用して、コンピューター上のすべてのバインディングのポートと拇印を確認します。 情報をディスクに出力するには、次の例に示すように、リダイレクト文字 ">" を使用します。  
  
    ```console  
    httpcfg query ssl>myMachinePorts.txt  
    ```
  
2. Windows Server 2003 または Windows XP では、HttpCfg.exe ツールと**delete**および**ssl**キーワードを使用します。 **-I**スイッチを使用して、 `IP` : `port` number を指定し、 **-h**スイッチを使用してサムプリントを指定します。  
  
    ```console  
    httpcfg delete ssl -i 0.0.0.0:8005 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6  
    ```  
  
3. Windows Vista では、次の例に示すように、Netsh.exe ツールを使用します。  
  
    ```console  
    Netsh http delete sslcert ipport=0.0.0.0:8005  
    ```  
  
## <a name="example"></a>例  

 次のコードは、トランスポート セキュリティを設定した <xref:System.ServiceModel.WSHttpBinding> クラスを使用して、自己ホスト型サービスを作成する方法を示します。 アプリケーションを作成する際、アドレス中にポート番号を指定してください。  
  
 [!code-csharp[c_WsHttpService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wshttpservice/cs/source.cs#3)]
 [!code-vb[c_WsHttpService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wshttpservice/vb/source.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [HTTP トランスポート セキュリティ](http-transport-security.md)
