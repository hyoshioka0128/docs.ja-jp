---
title: <socket> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/socket
- http://schemas.microsoft.com/.NetConfiguration/v2.0#socket
helpviewer_keywords:
- <socket> element
- socket element
ms.assetid: 366c634c-7d16-478f-aedf-053eda94a1a0
ms.openlocfilehash: 0e2b369eccfbc658a790ef61a961315a88361669
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "74089087"
---
# <a name="socket-element-network-settings"></a>\<socket> 要素 (ネットワーク設定)
ソケット操作が完了ポートを使用するかどうかを指定します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<socket>**

## <a name="syntax"></a>構文  
  
```xml  
<socket  
  alwaysUseCompletionPortsForConnect="true|false"  
  alwaysUseCompletionPortsForAccept="true|false"  
  ipProtectionLevel="EdgeRestricted|Restricted|Unrestricted|Unspecified"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`alwaysUseCompletionPortsForAccept`|Accept メソッド呼び出しに対して、ソケットが常に完了ポートを使用する必要があるかどうかを示します。 既定値は `false` です。|  
|`alwaysUseCompletionPortsForConnect`|接続メソッドの呼び出しで、ソケットが常に完了ポートを使用する必要があるかどうかを示します。 既定値は `false` です。|  
|`ipProtectionLevel`|ソケットに使用する既定のを指定し <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType> ます。 既定値は、Windows のバージョンによって異なります。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[設定](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>解説  
 `alwaysUseCompletionPortsForAccept`属性と `alwaysUseCompletionPortsForConnect` 属性は、名前空間のクラスによる完了ポートの使用に関する既定の動作を指定するために使用されます。 <xref:System.Net.Sockets?displayProperty=nameWithType> ハイパフォーマンスサーバーアプリケーションでは、完了ポートをお勧めします。  
  
 `alwaysUseCompletionPortsForAccept`属性と属性の既定値 `alwaysUseCompletionPortsForConnect` は**false**です。  
  
 は、 <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForAccept%2A> 適用可能な `alwaysUseCompletionPortsForAccept` 構成ファイルから属性の現在の値を取得するために使用できます。 は、 <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForConnect%2A> 適用可能な `alwaysUseCompletionPortsForConnect` 構成ファイルから属性の現在の値を取得するために使用できます。  
  
 属性は、 `ipProtectionLevel` ソケットに使用する既定のを指定し <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType> ます。 <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A>プロパティを使用すると、同じリンクローカルまたはサイトローカルプレフィックスを持つアドレスなど、指定されたスコープに IPv6 ソケットの制限を構成できます。 このオプションを使用すると、アプリケーションは IPv6 ソケットにアクセス制限を設けることができます。 この制限により、プライベート LAN で実行されるアプリケーションを外部からの攻撃に対して簡単かつ堅牢に強化できます。 このオプションは、リッスンしているソケットの範囲を拡大または縮小し、必要に応じてパブリックユーザーおよびプライベートユーザーからの無制限のアクセスを有効にするか、必要に応じて同じサイトへのアクセスのみを制限します。  
  
 この `ipProtectionLevel` 属性設定は、初期の受信トラフィックのみに影響します。  
  
- ソケットで着信接続をリッスンしている TCP サーバー。  
  
- ソケットでパケットを受信する UDP アプリケーション。  
  
 この構成設定は、既に確立されている TCP 接続には影響しません (トラフィックは両方向に制限されません)。また、UDP パケットを送信するアプリケーションには影響しません。  
  
 属性の設定に使用できる値は、次のよう `ipProtectionLevel` に、列挙で指定されている定義済みの保護レベルに対応してい <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType> ます。  
  
|**属性値**|**説明**|  
|-|-|  
|EdgeRestricted|IP 保護レベルはエッジ制限付きです。 この値は、インターネット経由で動作するように設計されているアプリケーションによって使用されます。 この設定を使用する場合、Windows Teredo 実装を使用したネットワーク アドレス変換 (NAT: Network Address Translation) トラバーサルは使用できません。 これらのアプリケーションは、IPv4 のファイアウォールをバイパスすることがあるため、開いているポートを対象としたインターネットからの攻撃に対して堅牢である必要があります。 Windows Server 2003 と Windows XP では、ソケットの IP 保護レベルの既定値はエッジ制限付きです。|  
|制限付き|IP 保護レベルは制限付きです。 この値は、インターネットのシナリオを実装しないイントラネット アプリケーションによって使用されます。 これらのアプリケーションは、一般的に、インターネット型の攻撃に対してテストが行われていなかったり堅牢ではなかったりします。 この設定を使用する場合、受信トラフィックはリンクローカルのみに制限されます。|  
|無制限|IP 保護レベルは無制限です。 この値は、Windows に組み込まれている IPv6 NAT Traversal 機能 (たとえば、Teredo) を使用するアプリケーションを含む、インターネット経由で動作するように設計されているアプリケーションによって使用されます。 これらのアプリケーションは、IPv4 のファイアウォールをバイパスすることがあるため、開いているポートを対象としたインターネットからの攻撃に対して堅牢である必要があります。 Windows Server 2008 R2 と Windows Vista では、ソケットの IP 保護レベルの既定値は無制限です。|  
|指定されていません。|IP 保護レベルは未指定です。 Windows 7 と Windows Server 2008 R2 では、ソケットの IP 保護レベルの既定値は未指定です。|  
  
 属性の既定値 `ipProtectionLevel` は**指定**されていません。  
  
 プロパティは、 <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A> `ipProtectionLevel` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、完了ポートを使用するように指定する方法と、既定値を無制限にすることを指定する方法を示し <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType> ます。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <socket  
        alwaysUseCompletionPortsForAccept="true"  
        alwaysUseCompletionPortsForConnect="true"  
        ipProtectionLevel="Unrestricted"  
       />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SocketElement?displayProperty=nameWithType>
- <xref:System.Net.Sockets?displayProperty=nameWithType>
- <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>
- <xref:System.Net.Sockets.SocketOptionName.IPProtectionLevel?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
