---
title: システムが提供するバインディングの構成
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], system-provided bindings
- WCF [WCF], system-provided bindings
- bindings [WCF], system-provided
ms.assetid: 443f8d65-f1f2-4311-83b3-4d8fdf7ccf16
ms.openlocfilehash: d6018c8339cb04471bf9ce0f2ee86e091e1d1e95
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597528"
---
# <a name="configuring-system-provided-bindings"></a>システムが提供するバインディングの構成
バインディングにより、エンドポイントとの通信で使用する通信メカニズムが指定され、エンドポイントへの接続方法が示されます。 バインディングは、Windows Communication Foundation (WCF) チャネルがどのように階層化され、必要な通信機能を提供するかを定義する要素で構成されます。 バインディングには次の 3 種類の要素が含まれます。  
  
- プロトコル チャネル バインド要素 : エンドポイントに送信されるメッセージで使用するセキュリティ、信頼性、コンテキスト フローの設定、またはユーザー定義のプロトコルを指定します。  
  
- トランスポート チャネル バインド要素 : エンドポイントにメッセージを送信するときに使用する基礎トランスポート プロトコル (TCP や HTTP など) を指定します。  
  
- メッセージ エンコーディング バインド要素 : エンドポイントに送信されるメッセージに使用するネットワーク エンコード (text/XML、バイナリ、MTOM (Message Transmission Optimization Mechanism) など) を指定します。  
  
 このトピックでは、システムによって提供されるすべての Windows Communication Foundation (WCF) バインドについて説明します。 このバインディングがいずれもアプリケーションの要件を満たさない場合は、<xref:System.ServiceModel.Channels.CustomBinding> クラスを使用してバインディングを作成できます。 カスタム バインドを作成する方法の詳細については、「[カスタム バインディング](../extending/custom-bindings.md)」を参照してください。  
  
> [!IMPORTANT]
> セキュリティが有効になっているバインディングを選択します。 既定では、<xref:System.ServiceModel.BasicHttpBinding> バインディング以外のバインディングではセキュリティが有効になっています。 セキュリティで保護されたバインディングを選択しない場合、またはセキュリティを無効にする場合は、セキュリティで保護されたデータ センターや隔離されたネットワークを使用するなど、他の方法でネットワーク交換が保護されていることを確認してください。  
  
> [!IMPORTANT]
> 他の方法によってネットワーク交換がセキュリティ保護されない限り、セキュリティをサポートしないバインディングやセキュリティが無効になっているバインディングでは、双方向コントラクトを使用しないでください。  
  
## <a name="system-provided-bindings"></a>システム標準のバインディング  
 次のバインディングは、WCF に付属しています。  
  
|バインド|Configuration 要素|説明|  
|-------------|---------------------------|-----------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md)|ASP.NET Web サービス (ASMX) ベースのサービスなど、WS-Basic Profile に適合する Web サービスとの通信に適したバインディング。 このバインディングはトランスポートとして HTTP を、既定のメッセージ エンコーディングとして text/XML を使用します。|  
|<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)|二重のサービス コントラクト以外に適した、セキュリティで保護された相互操作可能なバインディング。|  
|<xref:System.ServiceModel.WS2007HttpBinding>|[\<ws2007HttpBinding>](../../configure-apps/file-schema/wcf/ws2007httpbinding.md)|<xref:System.ServiceModel.WSHttpBinding.Security%2A>、<xref:System.ServiceModel.ReliableSession>、および <xref:System.ServiceModel.WSHttpBindingBase.TransactionFlow%2A> の各バインド要素の適切なバージョンをサポートする、セキュリティで保護された相互運用可能なバインディング。|  
|<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding>](../../configure-apps/file-schema/wcf/wsdualhttpbinding.md)|二重のサービス コントラクト、または SOAP 中継局を介しての通信に適した、セキュリティで保護された相互操作可能なバインディング。|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding>](../../configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|WS-Federation プロトコルをサポートする、セキュリティで保護された相互操作可能なバインディングで、フェデレーションに属す組織のユーザーを効率的に認証、および承認することができます。|  
|<xref:System.ServiceModel.WS2007FederationHttpBinding>|[\<ws2007FederationHttpBinding>](../../configure-apps/file-schema/wcf/ws2007federationhttpbinding.md)|<xref:System.ServiceModel.WS2007HttpBinding>から派生し、フェデレーション セキュリティをサポートする、セキュリティで保護された相互運用可能なバインディングです。|  
|<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)|WCF アプリケーション間でのコンピューター間通信に適した、セキュリティで保護され、最適化されたバインド。|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|[\<netNamedPipeBinding>](../../configure-apps/file-schema/wcf/netnamedpipebinding.md)|WCF アプリケーション間でのコンピューター上の通信に適した、セキュリティで保護され、信頼できる最適化されたバインド。|  
|<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding>](../../configure-apps/file-schema/wcf/netmsmqbinding.md)|WCF アプリケーション間でのコンピューター間通信に適した、キューに置かれたバインド。|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|[\<netPeerTcpBinding>](../../configure-apps/file-schema/wcf/netpeertcpbinding.md)|セキュリティで保護された、複数のコンピューター通信を可能にするバインディング。|  
|<xref:System.ServiceModel.WebHttpBinding>|[\<webHttpBinding>](../../configure-apps/file-schema/wcf/webhttpbinding.md)|SOAP メッセージではなく、HTTP 要求を介して公開される WCF Web サービスのエンドポイントを構成するために使用されるバインド。|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|[\<msmqIntegrationBinding>](../../configure-apps/file-schema/wcf/msmqintegrationbinding.md)|WCF アプリケーションと既存のメッセージキュー (MSMQ) アプリケーション間のコンピューター間通信に適したバインディング。|  
  
## <a name="binding-features"></a>バインディング機能  
 システム指定の各バインディングで提供される主要機能の一部を次の表に示します。 各バインディングを 1 列目に示します。機能に関する情報については表で説明します。 次の表に、使用されるバインディングの省略形のキーを示します。 バインディングを選択するには、必要な行の機能がすべて含まれる列を調べます。  
  
|バインド|相互運用性|セキュリティ モード (既定)|セッション<br /><br /> (既定)|トランザクション|二重|  
|-------------|----------------------|----------------------------------|-----------------------------|------------------|------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|Basic Profile 1.1|(なし)、トランスポート、メッセージ、混在|なし、(なし)|(なし)|該当なし|  
|<xref:System.ServiceModel.WSHttpBinding>|WS|なし、トランスポート、(メッセージ)、混在|(なし)、トランスポート、信頼できるセッション|(なし)、あり|該当なし|  
|<xref:System.ServiceModel.WS2007HttpBinding>|WS-Security、WS-Trust、WS-SecureConversation、WS-SecurityPolicy|なし、トランスポート、(メッセージ)、混在|(なし)、トランスポート、信頼できるセッション|(なし)、あり|該当なし|  
|<xref:System.ServiceModel.WSDualHttpBinding>|WS|なし、(メッセージ)|(信頼できるセッション)|(なし)、あり|はい|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|WS-Federation|なし、(メッセージ)、混在|(なし)、信頼できるセッション|(なし)、あり|いいえ|  
|<xref:System.ServiceModel.WS2007FederationHttpBinding>|WS-Federation|なし、(メッセージ)、混在|(なし)、信頼できるセッション|(なし)、あり|いいえ|  
|<xref:System.ServiceModel.NetTcpBinding>|.NET|なし、(トランスポート)、メッセージ、<br /><br /> 混在|信頼できるセッション、(トランスポート)|(なし)、あり|はい|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|.NET|なし、<br /><br /> (トランスポート)|なし、(トランスポート)|(なし)、あり|はい|  
|<xref:System.ServiceModel.NetMsmqBinding>|.NET|なし、メッセージ、(トランスポート)、両方|(なし)|(なし)、あり|いいえ|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|ピア|なし、メッセージ、(トランスポート)、混在|(なし)|(なし)|はい|  
|<xref:System.ServiceModel.WebHttpBinding>|.NET|None、Transport、TransportCredentialOnly|(なし)|(なし)|該当なし|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|MSMQ|なし、(トランスポート)|(なし)|(なし)、あり|該当なし|  
  
 次の表では、前の表内の機能について説明します。  
  
|機能|説明|  
|-------------|-----------------|  
|相互運用性の種類|バインディングによる相互操作を可能にするプロトコルまたはテクノロジに名前を付けます。|  
|Security|チャネルをセキュリティで保護する方法を指定します。<br /><br /> -None: SOAP メッセージはセキュリティで保護されておらず、クライアントは認証されていません。<br />-Transport: セキュリティ要件はトランスポート層で満たされます。<br />-Message: セキュリティ要件はメッセージ層で満たされています。<br />-Mixed: このセキュリティモードはと呼ばれ `TransportWithMessageCredentials` ます。 メッセージ レベルで資格情報を処理し、整合性と機密性の要件がトランスポート層で満たされます。<br />-Both: メッセージレベルとトランスポートレベルの両方のセキュリティが使用されます。 この機能は、<xref:System.ServiceModel.NetMsmqBinding> に特有の機能です。|  
|セッション|このバインディングでセッション コントラクトをサポートするかどうかを指定します。|  
|トランザクション|トランザクションが有効かどうかを指定します。|  
|二重|二重のコントラクトがサポートされているかどうかを指定します。 この機能はバインディングでセッションをサポートする必要があることに注意してください。|  
|ストリーミング|メッセージ ストリーミングをサポートするかどうかを指定します。|  
  
## <a name="see-also"></a>関連項目

- [エンドポイントの作成の概要](../endpoint-creation-overview.md)
- [サービスとクライアントを構成するためのバインディングの使用](../using-bindings-to-configure-services-and-clients.md)
- [基本的な WCF プログラミング](../basic-wcf-programming.md)
