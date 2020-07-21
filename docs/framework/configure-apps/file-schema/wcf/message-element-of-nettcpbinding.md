---
title: <message>の要素<netTcpBinding>
ms.date: 03/30/2017
ms.assetid: 1d71edd9-c085-4c2e-b6d3-980c313366f9
ms.openlocfilehash: 76c4a0a30b637bc168855b091029a959b858401e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73739011"
---
# <a name="message-element-of-nettcpbinding"></a>\<message>の要素\<netTcpBinding>
で構成されるエンドポイントのメッセージレベルのセキュリティ要件の種類を定義し [\<netTcpBinding>](nettcpbinding.md) ます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<netTcpBinding>**](nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<message>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<message algorithmSuite="System.Servicemodel.Security.SecurityAlgorithmsuite"
         clientCredentialType="None/Windows/UserName/Certificate/IssuedToken" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`algorithmSuite`|メッセージの暗号化とキー ラップ アルゴリズムを設定します。 アルゴリズムとキー サイズは、<xref:System.ServiceModel.Security.SecurityAlgorithmSuite> クラスにより決まります。 これらのアルゴリズムは、セキュリティ ポリシー言語 (WS-SecurityPolicy) 仕様で指定されたアルゴリズムにマップされます。<br /><br /> 次の表に、使用可能な値を示します。 既定値は `Basic256` です。<br /><br /> サービス バインディングで指定されている `algorithmSuite` 値が既定値と異なると、Svcutil.exe を使用して構成ファイルを生成したときにファイルが正しく生成されません。この場合は、構成ファイルを手動で編集して、この属性を適切な値に設定する必要があります。|  
|`clientCredentialType`|メッセージ ベースのセキュリティを使用してクライアント認証を実行するときに使用される資格情報の種類を指定します。 次の表に、使用可能な値を示します。 既定値は `UserName` です。 この属性は <xref:System.ServiceModel.MessageCredentialType> 型です。|  
  
## <a name="algorithmsuite-attribute"></a>algorithmSuite 属性  
  
|値|Description|  
|-----------|-----------------|  
|Basic128|Aes128 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic192|Aes192 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic256|Aes256 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic256Rsa15|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|Basic192Rsa15|メッセージの暗号化には Aes192 を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|TripleDes|TripleDes 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic128Rsa15|メッセージの暗号化には Aes128 を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|TripleDesRsa15|TripleDes 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|Basic128Sha256|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic192Sha256|メッセージの暗号化には Aes192 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic256Sha256|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|TripleDesSha256|メッセージの暗号化には TripleDes を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic128Sha256Rsa15|メッセージの暗号化には Aes128 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
|Basic192Sha256Rsa15|メッセージの暗号化には Aes192 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
|Basic256Sha256Rsa15|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
|TripleDesSha256Rsa15|メッセージの暗号化には TripleDes を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性  
  
|値|説明|  
|-----------|-----------------|  
|なし|サービスが匿名クライアントと対話できるようになります。 サービス側では、サービスがクライアントの資格情報を必要としないことを示しています。 クライアント側では、クライアントがクライアントの資格情報を提示しないことを示しています。|  
|Windows|SOAP 交換を、Windows 資格情報の認証されたコンテキストで行うことが可能になります。|  
|UserName|サービスが、UserName 資格情報を使用したクライアントの認証を要求できるようにします。 WCF では、パスワード ダイジェストの送信や、パスワードを使用したキーの派生およびこうしたキーの使用がサポートされません。これはメッセージのセキュリティを確保するためです。 そのため、ユーザー名の資格情報を使用する場合、WCF はトランスポートがセキュリティで保護されることを強制します。 この資格情報モードは、`negotiateServiceCredential` 属性に基づいて、同時実行可能な交換か、同時実行できないネゴシエーションのいずれかになります。|  
|Certificate|証明書を使用したクライアントの認証を、サービスで要求することが可能になります。 メッセージ セキュリティ モードが使用され、`negotiateServiceCredential` 属性が `false` に設定されている場合、クライアントにサービス証明書を準備する必要があります。|  
|IssuedToken|通常はセキュリティ トークン サービス (STS) により発行されるカスタム トークンを指定します。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|<xref:System.ServiceModel.Configuration.NetTcpBindingElement>のセキュリティ機能を定義します。|  
  
## <a name="remarks"></a>解説  
 メッセージは、SOAP メッセージの整合性と機密性を確保し、通信ピアの相互認証を行うために、メッセージ レベルのセキュリティを使用します。 バインディング上でこのセキュリティ モードが選択された場合、チャネル スタックは、メッセージ セキュリティ バインド要素を使用して構成され、SOAP メッセージは WS-Security* 標準に従って保護されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.MessageSecurityOverTcp>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement.Message%2A>
- <xref:System.ServiceModel.NetTcpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [バインド](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
