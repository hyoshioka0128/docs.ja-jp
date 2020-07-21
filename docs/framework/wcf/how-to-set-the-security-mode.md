---
title: '方法: セキュリティ モードを設定する'
description: ほとんどの定義済みバインディングで、トランスポート、メッセージ、および TransportWithMessageCredential の3つの一般的な WCF セキュリティモードを設定する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Mode property
- WCF, security mode
- WCF, security
ms.assetid: 6e01dd9f-b5dd-4474-b24c-06e124de4ff7
ms.openlocfilehash: 2f834e1930b7676592f6cbc29a577424d75ebc01
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244544"
---
# <a name="how-to-set-the-security-mode"></a>方法: セキュリティ モードを設定する

Windows Communication Foundation (WCF) セキュリティには、トランスポート、メッセージ、および "メッセージ資格情報によるトランスポート" のほとんどの定義済みバインディングで検出された3つの一般的なセキュリティモードがあります。 これ以外に、2 つのバインディングに固有の 2 つのモードがあります。<xref:System.ServiceModel.BasicHttpBinding> の "トランスポート資格情報専用" モードと、<xref:System.ServiceModel.NetMsmqBinding> の "両方" モードです。 ここでは、3 つの共通のセキュリティモードである <xref:System.ServiceModel.SecurityMode.Transport>、<xref:System.ServiceModel.SecurityMode.Message>、および <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential> に重点を置いて説明します。

ただし、これらのモードがすべての定義済みバインディングでサポートされるわけではありません。 ここでは、<xref:System.ServiceModel.WSHttpBinding> クラスと <xref:System.ServiceModel.NetTcpBinding> クラスでモードを設定し、プログラムと構成の両方を使用してモードを設定する方法を示します。

詳細については、「WCF セキュリティ」、「[セキュリティの概要](./feature-details/security-overview.md)」、「[サービス](securing-services.md)のセキュリティ保護」、および「[サービスとクライアント](./feature-details/securing-services-and-clients.md)のセキュリティ保護」を参照してください。 トランスポートモードとメッセージの詳細については、「[トランスポートセキュリティ](./feature-details/transport-security.md)と[メッセージセキュリティ](./feature-details/message-security-in-wcf.md)」を参照してください。

## <a name="to-set-the-security-mode-in-code"></a>コードでセキュリティ モードを設定するには

1. 使用しているバインディング クラスのインスタンスを作成します。 定義済みバインディングの一覧については、「[システム指定のバインディング](system-provided-bindings.md)」を参照してください。 この例では、<xref:System.ServiceModel.WSHttpBinding> クラスのインスタンスを作成します。

2. `Mode` プロパティから返されるオブジェクトの `Security` プロパティを設定します。

     [!code-csharp[c_SettingSecurityMode#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#1)]
     [!code-vb[c_SettingSecurityMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#1)]

     または、モードを Message (メッセージ) に設定します。コードは次のようになります。

     [!code-csharp[c_SettingSecurityMode#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#2)]
     [!code-vb[c_SettingSecurityMode#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#2)]

     または、モードを TransportWithMessageCredential (メッセージ資格情報付きトランスポート) に設定します。コードは次のようになります。

     [!code-csharp[c_SettingSecurityMode#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#3)]
     [!code-vb[c_SettingSecurityMode#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#3)]

3. 次のコードに示すように、バインディングのコンストラクターでモードを設定することもできます。

     [!code-csharp[c_SettingSecurityMode#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#4)]
     [!code-vb[c_SettingSecurityMode#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#4)]

## <a name="setting-the-clientcredentialtype-property"></a>ClientCredentialType プロパティの設定

モードを上記の 3 つの値のいずれかに設定すると、`ClientCredentialType` プロパティの設定方法が決まります。 たとえば、<xref:System.ServiceModel.WSHttpBinding> クラスを使用し、モードを `Transport` に設定した場合、<xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> クラスの <xref:System.ServiceModel.HttpTransportSecurity> プロパティを適切な値に設定する必要があります。

### <a name="to-set-the-clientcredentialtype-property-for-transport-mode"></a>トランスポート モードの ClientCredentialType プロパティを設定するには

1. バインディングのインスタンスを作成します。

2. `Mode` プロパティを `Transport`に設定します。

3. `ClientCredential` プロパティに適切な値を設定します。 プロパティを `Windows` に設定するコードを次に示します。

     [!code-csharp[c_SettingSecurityMode#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#5)]
     [!code-vb[c_SettingSecurityMode#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#5)]

### <a name="to-set-the-clientcredentialtype-property-for-message-mode"></a>メッセージ モードの ClientCredentialType プロパティを設定するには

1. バインディングのインスタンスを作成します。

2. `Mode` プロパティを `Message`に設定します。

3. `ClientCredential` プロパティに適切な値を設定します。 プロパティを `Certificate` に設定するコードを次に示します。

     [!code-csharp[c_SettingSecurityMode#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#6)]
     [!code-vb[c_SettingSecurityMode#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#6)]

### <a name="to-set-the-mode-and-clientcredentialtype-property-in-configuration"></a>構成でモードと ClientCredentialType プロパティを設定するには

1. 構成ファイルの要素に適切なバインド要素を追加 [\<bindings>](../configure-apps/file-schema/wcf/bindings.md) します。 次の例では、要素を追加し [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) ます。

2. 要素を追加 `<binding>` し、その `name` 属性を適切な値に設定します。

3. `<security>` 要素を追加し、`mode` 属性を `Message`、`Transport`、または `TransportWithMessageCredential` に設定します。

4. モードを `Transport` に設定した場合は、`<transport>` 要素を追加し、`clientCredential` 属性を適切な値に設定します。

     モードを "`Transport"` に設定し、`clientCredentialType` 要素の `<transport>` 属性を "`Windows"` に設定する例を次に示します。

    ```xml
    <wsHttpBinding>
    <binding name="TransportSecurity">
        <security mode="Transport" >
           <transport clientCredentialType = "Windows" />
        </security>
    </binding>
    </wsHttpBinding >
    ```

     または、`security mode` を "`Message"` に設定し、その後に `<"message">` 要素を指定します。 この例では、`clientCredentialType` を "`Certificate"` に設定しています。

    ```xml
    <wsHttpBinding>
    <binding name="MessageSecurity">
        <security mode="Message" >
           <message clientCredentialType = "Certificate" />
        </security>
    </binding>
    </wsHttpBinding >
    ```

     次に説明する <xref:System.ServiceModel.BasicHttpSecurityMode.TransportWithMessageCredential> 値は、特殊なケースで使用されます。

### <a name="using-transportwithmessagecredential"></a>TransportWithMessageCredential の使用

セキュリティ モードを `TransportWithMessageCredential` に設定した場合、トランスポート レベルのセキュリティを提供する実際の機構はトランスポートによって決まります。 たとえば、HTTP プロトコルでは SSL (Secure Sockets Layer) over HTTP (HTTPS) を使用します。 このため、トランスポート セキュリティ オブジェクト (`ClientCredentialType` など) の <xref:System.ServiceModel.HttpTransportSecurity> プロパティを設定しても無視されます。  つまり、メッセージ セキュリティ オブジェクト (`ClientCredentialType` バインディングの場合は `WSHttpBinding` オブジェクト) の <xref:System.ServiceModel.NonDualMessageSecurityOverHttp> だけを設定できます。

詳細については、「[方法: トランスポートセキュリティとメッセージ資格情報を使用](./feature-details/how-to-use-transport-security-and-message-credentials.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: SSL 証明書を使用してポートを構成する](./feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)
- [方法: トランスポート セキュリティとメッセージ資格情報を使用する](./feature-details/how-to-use-transport-security-and-message-credentials.md)
- [トランスポートセキュリティ](./feature-details/transport-security.md)
- [メッセージのセキュリティ](./feature-details/message-security-in-wcf.md)
- [セキュリティの概要](./feature-details/security-overview.md)
- [システム標準のバインディング](system-provided-bindings.md)
- [\<security>](../configure-apps/file-schema/wcf/security-of-wshttpbinding.md)
- [\<security>](../configure-apps/file-schema/wcf/security-of-basichttpbinding.md)
- [\<security>](../configure-apps/file-schema/wcf/security-of-nettcpbinding.md)
