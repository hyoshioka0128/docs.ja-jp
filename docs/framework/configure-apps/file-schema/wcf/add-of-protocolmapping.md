---
title: <add> の <protocolMapping>
ms.date: 03/30/2017
ms.assetid: 08e62249-1641-41d1-91b1-66d7b46244e4
ms.openlocfilehash: 6197d01665d49a7c97ac9e44251abf15faf80a8f
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70850385"
---
# <a name="add-of-protocolmapping"></a>\<add> の \<protocolMapping>
トランスポートプロトコルスキーム (http、net.tcp、net.pipe など) と Windows Communication Foundation (WCF) バインドとの間の既定のプロトコルマッピングを表します。 実行時に既定のエンドポイントを作成する場合、WCF は構成されたマッピングを調べ、特定のベースアドレスに使用するバインドを決定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<protocolMapping>**](protocolmapping.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<protocolMapping>
  <add binding="String"
       bindingConfiguration="String"
       scheme="http/net.msmq/net.pipe/net.tcp" />
</protocolMapping>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|要素|説明|  
|-------------|-----------------|  
|binding|既定のエンドポイントを作成するときにエンドポイントに使用されるバインディングの種類を指定する文字列。|  
|bindingConfiguration|参照されるバインディング構成セクションの名前を指定する文字列。|  
|scheme|既定のエンドポイントに使用されるトランスポート プロトコル スキーム。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<protocolMapping>](protocolmapping.md)|トランスポートプロトコルスキーム (http、net.tcp、net.pipe など) と Windows Communication Foundation (WCF) バインド間の既定のプロトコルマッピングを定義するための構成セクションを表します。|  
  
## <a name="example"></a>例  
 次の構成例は、machine.config ファイル内の既定のプロトコル マッピングを示しています。 machine.config ファイルを変更することで、既定のマッピングをコンピューター レベルでオーバーライドできます。 または、アプリケーションのスコープ内だけでオーバーライドする場合は、アプリケーション構成ファイルのこのセクションをオーバーライドし、各プロトコル スキームのマッピングを変更できます。  
  
```xml  
<protocolMapping>
  <add scheme="http"
       binding="basicHttpBinding" />
  <add scheme="net.tcp"
       binding="netTcpBinding" />
  <add scheme="net.pipe"
       binding="netNamedPipeBinding" />
  <add scheme="net.msmq"
       binding="netMsmqBinding" />
</protocolMapping>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ProtocolMappingSection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Configuration.ProtocolMappingElement?displayProperty=nameWithType>
