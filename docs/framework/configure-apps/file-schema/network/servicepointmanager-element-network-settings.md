---
title: <servicePointManager> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#servicePointManager
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/servicePointManager
helpviewer_keywords:
- servicePointManager element
- <servicePointManager> element
ms.assetid: 6e5def51-3646-4ef6-a7bd-c69151321bec
ms.openlocfilehash: 95ad1880cbb832a17311e7e63e9203f53257f65f
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697713"
---
# <a name="servicepointmanager-element-network-settings"></a>\<servicePointManager > 要素 (ネットワーク設定)
ネットワークリソースへの接続を構成します。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t 47 >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t @ no__t @no__t @ no__t-3[ **-6 設定 >** ](settings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 **\<servicePointManager** (&) >  
  
## <a name="syntax"></a>構文  
  
```xml  
<servicePointManager  
  checkCertificateName="true|false"  
  checkCertificateRevocationList="true|false"  
  encryptionPolicy="AllowNoEncryption|NoEncryption|RequireEncryption"  
  expect100Continue="true|false"  
  useNagleAlgorithm="true|false"  
  enableDnsRoundRobin="true|false"  
  dnsRefreshTimeout="time"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**[説明]**|  
|-------------------|---------------------|  
|`checkCertificateName`|証明書を使用する前に、証明書の名前がサーバーホスト名と一致するかどうかをシステムが確認する必要があるかどうかを指定します。 既定値は `true` です。|  
|`checkCertificateRevocationList`|証明書を使用する前に証明書が失効しているかどうかをシステムが確認するかどうかを指定します。 既定値は `false` です。|  
|`dnsRefreshTimeout`|DNS ラウンドロビンオプションと共に、ドメインネームサービス (DNS) の解決時間をミリ秒単位でキャッシュする期間を指定します。 既定値は 120,000 ミリ秒 (2 分) です。|  
|`enableDnsRoundRobin`|複数のインターネットプロトコル (IP) アドレスを持つホスト名の DNS 解決が、すべてのアドレスを返すのか、それとも1つだけを返すのかを指定します。 既定値は `false` です。|  
|`encryptionPolicy`|@No__t 0 のインスタンスの SSL/TLS セッションに適用される暗号化ポリシーを指定します。 指定できる値は、<xref:System.Net.Security.EncryptionPolicy> 列挙体の値と同じです。 暗号化ポリシーが `NoEncryption` に設定されている場合は、<xref:System.Security.Authentication.CipherAlgorithmType.Null> を使用する必要があります。 既定値は `RequireEncryption` です。|  
|`expect100Continue`|POST メソッドがサーバーからの `100-continue` 応答を受信する必要があるかどうかを指定します。 既定値は `true` です。|  
|`useNagleAlgorithm`|サービスポイントマネージャーによって制御される接続が Nagle アルゴリズムを使用するかどうかを指定します。 既定値は `true` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**[説明]**|  
|-----------------|---------------------|  
|[[設定]](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.ServicePointManager>
- <xref:System.Net.Security.EncryptionPolicy>
- [ネットワーク設定スキーマ](index.md)
