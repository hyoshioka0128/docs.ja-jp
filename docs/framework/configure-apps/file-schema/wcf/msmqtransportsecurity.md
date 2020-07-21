---
title: <msmqTransportSecurity>
ms.date: 03/30/2017
ms.assetid: 092e911b-ab1b-4069-a26e-6134c3299e06
ms.openlocfilehash: 5899c609b3cf52c4a275ba6fb10c5826fcf37f1e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153010"
---
# \<msmqTransportSecurity>
カスタム バインディングの MSMQ トランスポート セキュリティ設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<msmqIntegration>**](msmqintegration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<msmqTransportSecurity>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<msmqTransportSecurity msmqAuthenticationMode="None/Windows/Certificate"
                       msmqEncryptionAlgorithm="RC4Stream/AES"
                       msmqProtectionLevel="None/Sign/EncryptAndSign"
                       msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />
</msmqTransportSecurity>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`msmqAuthenticationMode`|MSMQ トランスポートによるメッセージの認証方法を指定します。 これが `None` に設定されている場合、`msmqProtectionLevel` 属性の値も `None` に設定する必要があります。<br /><br /> 有効な値は次のとおりです。<br /><br /> -None: 認証なし。<br />-Windows: 認証メカニズムは Active Directory を使用して、メッセージに関連付けられている SID の x.509 証明書を取得します。 次に、これを使用してキューの ACL がチェックされ、ユーザーがキューに書き込む権限を持っていることが確認されます。<br />-Certificate: チャネルは、証明書ストアから証明書を取得します。<br /><br /> 既定値は Windows です。 この属性は <xref:System.ServiceModel.MsmqAuthenticationMode> 型です。|  
|`msmqEncryptionAlgorithm`|メッセージ キュー マネージャー間でメッセージを転送するときに、ネットワーク上でメッセージの暗号化に使用されるアルゴリズムを指定します。 有効な値は次のとおりです。<br /><br /> - RC4Stream<br />-AES<br /><br /> 既定値は RC4Stream です。 この属性は <xref:System.ServiceModel.MsmqEncryptionAlgorithm> 型です。|  
|`msmqProtectionLevel`|MSMQ トランスポートのレベルでメッセージをセキュリティで保護する方法を指定します。 暗号化によってメッセージの整合性が確保されますが、EncryptAndSign ではメッセージの整合性と否認不可が保証されます。つまり、メッセージは実際には送信者から送信され、送信者はそのことを伝えるものです。 有効な値は次のとおりです。<br /><br /> -None: 保護がありません。<br />-Sign: メッセージは署名されています。<br />-EncryptAndSign: メッセージは暗号化され、署名されます。<br /><br /> 既定値は Sign です。 この属性は <xref:System.Net.Security.ProtectionLevel> 型です。|  
|`msmqSecureHashAlgorithm`|署名の一部としてダイジェストの計算に使用されるアルゴリズムを指定します。 有効な値は次のとおりです。<br /><br /> -MD5<br />-SHA1<br />-SHA256<br />-SHA512<br /><br /> 既定値は SHA1 です。 この属性は <xref:System.ServiceModel.MsmqSecureHashAlgorithm> 型です。<br>MD5 と SHA1 の衝突の問題のため、SHA256 以上をお勧めします。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<msmqIntegration>](msmqintegration.md)|Message Queuing (MSMQ) の送信側または受信側とのやり取りに必要な設定を指定します。|  
|[\<msmqTransport>](msmqtransport.md)|ネイティブ MSMQ プロトコルを使用する Windows Communication Foundation (WCF) サービスのキュー通信プロパティを指定します。|  
  
## <a name="remarks"></a>解説  
 トランスポートセキュリティの詳細については、「[トランスポートセキュリティ](../../../wcf/feature-details/transport-security.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity>
- <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [WCF のキュー](../../../wcf/feature-details/queues-in-wcf.md)
- [トランスポート](../../../wcf/feature-details/transports.md)
- [トランスポートの選択](../../../wcf/feature-details/choosing-a-transport.md)
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [トランスポートセキュリティ](../../../wcf/feature-details/transport-security.md)
