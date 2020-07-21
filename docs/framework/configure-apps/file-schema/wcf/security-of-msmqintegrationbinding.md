---
title: <security> の <msmqIntegrationBinding>
ms.date: 03/30/2017
ms.assetid: ae5c68a8-14a2-4c6e-b9e0-3e94e3e9135e
ms.openlocfilehash: 2268bf48a2b86c3b3b25db006e6f8f55ea33af73
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73738684"
---
# <a name="security-of-msmqintegrationbinding"></a>\<security> の \<msmqIntegrationBinding>
メッセージ キュー (MSMQ) 統合チャネルのトランスポート セキュリティ設定を定義します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<msmqIntegrationBinding>**](msmqintegrationbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<security>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<msmqIntegrationBinding>
  <binding>
    <security mode="None/Transport">
      <transport msmqAuthenticationMode="None/Windows/Certificate"
                 msmqEncryptionAlgorithm="RC4Stream/AES"
                 msmqProtectionLevel="None/Sign/EncryptAndSign"
                 msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />
      <message algorithmSuite="Aes128/Aes192/Aes256/Rsa15Aes128/ Rsa15Aes256/TripleDes"
               clientCredentialType="None/Windows/UserName/Certificate/CardSpace"
               defaultProtectionLevel="None/Sign/EncryptAndSign" />
    </security>
  </binding>
</msmqIntegrationBinding>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|mode|メッセージ キュー統合チャネルの整合性、機密性、および認証を制御するセキュリティの種類を指定します。 有効な値は次のとおりです。<br /><br /> -None: セキュリティを無効にします。<br />-Transport: 保護と認証はトランスポートによって提供されます。 これは、2 つのキュー マネージャー間のメッセージ セキュリティに適用されます。 アプリケーションとキュー マネージャーとの間にセキュリティは提供されません。 既存の Msmq アプリケーションは、この種類のセキュリティ モードと機能的に等価です。<br /><br /> 既定値は `Transport` です。 この属性は <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurityMode> 型です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<transport>](transport-of-msmqintegrationbinding.md)|メッセージ キュー統合トランスポートのセキュリティ設定を定義します。 この要素は <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|のバインディング要素 [\<msmqIntegrationBinding>](msmqintegrationbinding.md) 。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement>
- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.MsmqIntegrationBindingElement.Security%2A>
- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity>
- [WCF のキュー](../../../wcf/feature-details/queues-in-wcf.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [バインド](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
- [\<msmqIntegrationBinding>](msmqintegrationbinding.md)
