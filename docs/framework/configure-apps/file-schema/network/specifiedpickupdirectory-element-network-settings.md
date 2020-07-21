---
title: <specifiedPickupDirectory> 要素 (ネットワーク設定)
description: <specifiedPickupDirectory>Network settings 要素は、.NET Framework の SMTP サーバーオプションのローカルディレクトリを構成します。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#specifiedPickupDirectory
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/specifiedPickupDirectory
helpviewer_keywords:
- specifiedPickupDirectory element
- <specifiedPickupDirectory> element
ms.assetid: 0121f49d-bff2-4bc6-af06-f1628dcd61f1
ms.openlocfilehash: f0c4c1845e9542d0f3b836ff03f16bdf2979ebd8
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504499"
---
# <a name="specifiedpickupdirectory-element-network-settings"></a>\<specifiedPickupDirectory> 要素 (ネットワーク設定)
SMTP (Simple Mail Transport Protocol) サーバー用のローカル ディレクトリを設定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<mailSettings>**](mailsettings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<smtp>**](smtp-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<specifiedPickupDirectory>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<specifiedPickupDirectory  
  pickupDirectoryLocation="directory"
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`pickupDirectoryLocation`|アプリケーションが SMTP サーバーによって後で処理するために電子メールを保存するディレクトリ。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<smtp>要素 (ネットワーク設定)](smtp-element-network-settings.md)|SMTP (Simple Mail Transport Protocol) メール送信オプションを構成します。|  
  
## <a name="remarks"></a>解説  
 属性は、 `specifiedPickupDirectory` アプリケーションが SMTP サーバーによって処理されるメールメッセージを保存するディレクトリを設定します。  
  
## <a name="example"></a>例  
 次の例では、電子メールのピックアップディレクトリとして c:\ maildrop を指定します。  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="SpecifiedPickupDirectory">  
        <specifiedPickupDirectory  
          pickupDirectoryLocation="c:\maildrop"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SmtpSpecifiedPickupDirectoryElement?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
