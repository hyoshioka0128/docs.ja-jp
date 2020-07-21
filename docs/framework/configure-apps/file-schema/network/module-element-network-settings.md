---
title: <module> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#module
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/module
helpviewer_keywords:
- module element
- <module> element
ms.assetid: 10318725-9666-4d65-ab61-b94c64e59f13
ms.openlocfilehash: ed28ae4a52085cbfa781b4baf2ee1eafbeff6eb4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154830"
---
# <a name="module-element-network-settings"></a>\<module> 要素 (ネットワーク設定)
新しいプロキシ モジュールをアプリケーションに追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<defaultProxy>**](defaultproxy-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<module>**

## <a name="syntax"></a>構文  
  
```xml  
<module
  type="type_fullname, assembly_fullname"
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`type`|プロキシを実装する、(プロパティによって示される) 完全修飾型名 <xref:System.Type.FullName%2A> と、コンマで区切られたアセンブリ名 (プロパティによって示され <xref:System.Reflection.Assembly.FullName%2A> ます)。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[defaultProxy](defaultproxy-element-network-settings.md)|ハイパーテキスト転送プロトコル (HTTP: Hypertext Transfer Protocol) プロキシ サーバーを構成します。|  
  
## <a name="remarks"></a>解説  
 要素は、 `module` インターフェイスを実装するプロキシクラスを登録し <xref:System.Net.IWebProxy> ます。 プロキシクラスを登録した後、を `module` 使用して、サポートされているプロキシ経由で情報を要求できます。  
  
 属性の値は、 `type` モジュールのクラス名と、対応するダイナミックリンクライブラリ (DLL) の名前にする必要があります。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、カスタムプロキシクラスを登録します。  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <module  
        type="Test.CustomWebProxy, TestProxy, Version=2.0.3600.0, Culture=neutral, PublicKeyToken=b23a5c561934e385"  
      />  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.IWebProxy?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
