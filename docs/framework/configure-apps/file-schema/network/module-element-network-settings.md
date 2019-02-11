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
ms.openlocfilehash: 4658af3f55bddb5f5a748db5366c53f1d2733983
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55268198"
---
# <a name="module-element-network-settings"></a>\<module> 要素 (ネットワーク設定)
新しいプロキシ モジュールをアプリケーションに追加します。  
  
\<configuration>  
\<system.net>  
\<defaultProxy>  
\<module>  
  
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
|`type`|完全修飾型名 (によって示される、<xref:System.Type.FullName%2A>プロパティ) とアセンブリ名 (によって示される、<xref:System.Reflection.Assembly.FullName%2A>プロパティ)、プロキシを実装する、コンマで区切られました。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|ハイパーテキスト転送プロトコル (HTTP: Hypertext Transfer Protocol) プロキシ サーバーを構成します。|  
  
## <a name="remarks"></a>Remarks  
 `module`要素を実装するプロキシ クラスの登録、<xref:System.Net.IWebProxy>インターフェイス。 プロキシ クラスを登録した後`module`サポートされているプロキシを使用して情報を要求するために使用できます。  
  
 値、`type`属性がモジュールのクラス名と名前の対応するダイナミック リンク ライブラリ (DLL) にする必要があります。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、カスタムのプロキシ クラスを登録します。  
  
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
- [ネットワーク設定スキーマ](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
