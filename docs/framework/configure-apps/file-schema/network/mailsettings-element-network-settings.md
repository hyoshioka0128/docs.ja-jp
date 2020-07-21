---
title: <mailSettings> 要素 (ネットワーク設定)
description: <mailSettings>Network settings 要素は、.NET Framework のメール送信オプションを構成します。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings
helpviewer_keywords:
- mailSettings element
- <mailSettings> element
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
ms.openlocfilehash: ce7b8564e4ee5ea73d42259612c077420d36645b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504564"
---
# <a name="mailsettings-element-network-settings"></a>\<mailSettings> 要素 (ネットワーク設定)
電子メールの送信オプションを設定します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<mailSettings>**

## <a name="syntax"></a>構文  
  
```xml  
<mailSettings>
  <smtp>...</smtp>  
</mailSettings>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|属性|説明|  
|---------------|-----------------|  
|[\<smtp>要素 (ネットワーク設定)](smtp-element-network-settings.md)|簡易メール転送プロトコルのオプションを構成します。|  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[\<system.Net>要素 (ネットワーク設定)](system-net-element-network-settings.md)|.NET Framework がネットワークに接続する方法を指定するための設定が含まれています。|  
  
## <a name="example"></a>例  
 次の例では、既定のネットワーク資格情報を使用して電子メールを送信するための適切な SMTP パラメーターを指定しています。  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Mail.SmtpClient>
- [ネットワーク設定スキーマ](index.md)
