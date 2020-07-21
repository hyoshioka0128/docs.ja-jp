---
title: <chunkedCookieHandler>
ms.date: 03/30/2017
ms.assetid: 7220de45-1d14-4aec-a29e-4a2ea8ac861f
author: BrucePerlerMS
ms.openlocfilehash: 6aad95033b99f1472284f838f3ede2e74ea8324c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252105"
---
# \<chunkedCookieHandler>
を構成 <xref:System.IdentityModel.Services.ChunkedCookieHandler> します。 この要素は `mode` 、要素の属性 `<cookieHandler>` が "Default" または "Chunked" の場合にのみ存在する可能性があります。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<federationConfiguration>**](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<cookieHandler>**](cookiehandler.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<chunkedCookieHandler>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Chunked||Default" >  
      <chunkedCookieHandler size=xs:int >  
      </chunkedCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|chunkSize|1つの HTTP クッキーの HTTP クッキーデータの最大サイズ (文字数)。 チャンクサイズを調整する場合は注意が必要です。 Web ブラウザーでは、cookie のサイズとドメインごとに許可される数の制限が異なります。 たとえば、元の Netscape 仕様では、これらの制限が規定されています。これは、cookie の合計数は300クッキー、cookie ヘッダーあたりは4096バイト (cookie の値だけでなく、メタデータを含む)、ドメインごとに20の cookie です。 既定値は 2000 です。 必須。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<cookieHandler>](cookiehandler.md)|<xref:System.IdentityModel.Services.CookieHandler> <xref:System.IdentityModel.Services.SessionAuthenticationModule> (SAM) が cookie の読み取りと書き込みに使用するを構成します。|  
  
## <a name="remarks"></a>解説  
 <xref:System.IdentityModel.Services.ChunkedCookieHandler> `mode` 要素の属性を `<cookieHandler>` "Default" または "Chunked" に設定してを指定した場合、子要素を追加し、その属性を設定することにより、cookie ハンドラーが cookie の読み書きに使用するチャンクサイズを指定でき `<chunkedCookieHandler>` `chunkSize` ます。 `<chunkedCookieHandler>`要素が存在しない場合は、既定のチャンクサイズである2000バイトが使用されます。 `mode`属性が "Custom" に設定されている場合、この要素を指定することはできません。  
  
 `<chunkedCookieHandler>`要素は、クラスによって表され <xref:System.IdentityModel.Services.ChunkedCookieHandlerElement> ます。  
  
## <a name="example"></a>例  
 次の例では、3000バイトのチャンク単位でクッキーを書き込むチャンク cookie ハンドラーを構成します。  
  
```xml  
<cookieHandler mode="Chunked">  
    <chunkedCookieHandler chunkSize=3000/>  
</cookieHandler>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Services.ChunkedCookieHandler>
