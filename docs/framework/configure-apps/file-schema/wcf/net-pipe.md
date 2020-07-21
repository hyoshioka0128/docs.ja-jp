---
title: <net.pipe>
ms.date: 03/30/2017
ms.assetid: 6a0f0318-f8f6-466c-9fae-199d7274a82e
ms.openlocfilehash: dd984b2ab89060451b1b2d02c324e803766908ce
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70397724"
---
# \<net.pipe>
名前付きパイプ接続の有効期間を管理し、名前付きパイプを介して到着するアクティベーション要求を処理する名前付きパイプ アクティベーション サービスの構成設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel.activation>**](system-servicemodel-activation.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<net.pipe>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<configuration>
  <system.serviceModel.activation>
    <net.pipe maxPendingAccepts="Integer"
              maxPendingConnections="Integer"
              receiveTimeout="TimeSpan">
      <allowAccounts>
        <!-- LocalSystem account -->
        <add securityIdentifier="S-1-5-18" />
        <!-- LocalService account -->
        <add securityIdentifier="S-1-5-19" />
        <!-- Administrators account -->
        <add securityIdentifier="S-1-5-20" />
        <!-- Network Service account -->
        <add securityIdentifier="S-1-5-32-544" />
        <!-- IIS_IUSRS account (Vista only) -->
        <add securityIdentifier="S-1-5-32-568" />
      </allowAccounts>
    </net.pipe>
  </system.serviceModel.activation>
</configuration>
```  
  
## <a name="type"></a>Type  
 `Type`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`maxPendingAccepts`|整数は、共有サービスの待機エンドポイントで同時に受け入れる未処理のスレッドの最大数を示しています。 既定値は 2 です。|  
|`maxPendingConnections`|ディスパッチを待機できる最大接続数を指定する整数。 既定値は、100 です。|  
|`receiveTimeout`|フレーム データを読み取り、基礎となる接続から接続ディスパッチを実行するタイムアウトを指定する <xref:System.TimeSpan> です。 既定値は "00:00:10" です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<allowAccounts>](allowaccounts.md)|`securityIdentifier`WCF サービスをホストするプロセスのユーザーアカウントを指定する属性を含む構成要素のコレクション。共有サービスへの接続アクセス権が付与されます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<system.serviceModel.activation>](system-servicemodel-activation.md)|リスナー プロセス SMSvcHost.exe の設定が含まれています。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activation.Configuration.NetPipeSection>
