---
title: <localServiceSettings> 要素
ms.date: 03/30/2017
ms.assetid: 0658549c-3f65-46dd-8c5c-9895441ed734
ms.openlocfilehash: 4883fd563ecf989d67c369085df4fc43d0c5f078
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400304"
---
# <a name="localservicesettings-element"></a>\<localServiceSettings> 要素
このバインディングのローカル サービスのセキュリティ設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<localServiceSettings>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<security>
  <localServiceSettings detectReplays="Boolean"
                        inactivityTimeout="TimeSpan"
                        issuedCookieLifeTime="TimeSpan"
                        maxCachedCookies="Integer"
                        maxClockSkew="TimeSpan"
                        maxPendingSessions="Integer"
                        maxStatefulNegotiations="Integer"
                        negotiationTimeout="TimeSpan"
                        reconnectTransportOnFailure="Boolean"
                        replayCacheSize="Integer"
                        replayWindow="TimeSpan"
                        sessionKeyRenewalInterval="TimeSpan"
                        sessionKeyRolloverInterval="TimeSpan"
                        timestampValidityDuration="TimeSpan" />
</security>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`detectReplays`|チャネルに対するリプレイ攻撃を検出し、自動的に処理するかどうかを指定するブール値です。 既定値は、`false` です。|  
|`inactivityTimeout`|<xref:System.TimeSpan>チャネルがタイムアウトまで待機する非アクティブな時間を指定する正の。既定値は "01:00:00" です。|  
|`issuedCookieLifeTime`|すべての新しいセキュリティ クッキーに発行される有効期間を指定する <xref:System.TimeSpan>。 有効期間を超えるクッキーは、再利用され、再度ネゴシエートされる必要があります。 既定値は、"10:00:00" です。|  
|`maxCachedCookies`|キャッシュできるクッキーの最大数を指定する正の整数。 既定値は 1000 です。|  
|`maxClockSkew`|通信している双方の 2 つのシステム クロックのずれの最長時間を指定する <xref:System.TimeSpan>。 既定値は、"00:05:00" です。<br /><br /> この値が既定値に設定されている場合、受信側はメッセージが受信された時間より前後最大 5 分間の送信時間タイム スタンプを持つメッセージを受け入れます。 送信時間テストにパスしないメッセージは拒否されます。 この設定は、`replayWindow` 属性と組み合わせて使用します。|  
|`maxPendingSessions`|サービスがサポートする保留状態のセキュリティ セッションの最大数を指定する正の整数。 この制限に達すると、すべての新しいクライアントが SOAP エラーを受け取ります。 既定値は 1000 です。|  
|`maxStatefulNegotiations`|同時にアクティブにできるセキュリティ ネゴシエーションの数を指定する正の整数。 制限を超えるネゴシエーション セッションはキューに置かれ、制限内に空きができた場合にのみ完了できます。 既定値は 1024 です。|  
|`negotiationTimeout`|チャネルによって使用されるセキュリティ ポリシーの有効期間を指定する <xref:System.TimeSpan>。 有効期間が切れると、チャネルは新しいセキュリティ ポリシーについてクライアントと再度ネゴシエートします。 既定値は、"00:02:00" です。|  
|`reconnectTransportOnFailure`|WS-ReliableMessaging を使用した接続が、トランスポート エラーの後再接続を試みるかどうかを指定するブール値です。 既定値は `true` です。これは、再接続の試行が無限に行われることを意味します。 循環は非アクティブ タイムアウトにより破棄され、再接続できない場合はチャネルが例外をスローします。|  
|`replayCacheSize`|リプレイ検証で使用される、キャッシュ済みの nonce 数を指定する正の整数。 この制限を越えると、最も古い nonce が削除され、新しいメッセージ用に新しい nonce が作成されます。 既定値は 500000 です。|  
|`replayWindow`|個別のメッセージ nonce の有効期間を指定する <xref:System.TimeSpan>。<br /><br /> この期間が過ぎると、以前に送信されたメッセージと同じ nonce を持つメッセージは受け入れられません。 この属性は、リプレイ攻撃を防ぐために `maxClockSkew` 属性と組み合わせて使用します。 攻撃者は、メッセージのリプレイ ウィンドウの期限が切れた後にメッセージをリプレイする可能性があります。 ただし、このメッセージは `maxClockSkew` テストに失敗します。このテストは、メッセージが受信された時間の前後指定時間以内の送信時間タイムスタンプを持つメッセージを拒否します。|  
|`sessionKeyRenewalInterval`|イニシエーターがセキュリティ セッションのキーを更新するまでの期間を指定する <xref:System.TimeSpan>。 既定値は "10:00:00" です。|  
|`sessionKeyRolloverInterval`|キーの更新中に、前のセッション キーが受信メッセージで有効な時間間隔を指定する <xref:System.TimeSpan> です。 既定値は "00:05:00" です。<br /><br /> キーの更新中、クライアントおよびサーバーは、常に、利用可能な最新のキーを使用してメッセージを送信する必要があります。 どちらのパーティも、ロールオーバー時間に達するまで、前のセッション キーで保護された受信メッセージを受け入れます。|  
|`timestampValidityDuration`|タイムスタンプの有効期間を指定する正の <xref:System.TimeSpan>。 既定値は "00:15:00" です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<security>](security-of-custombinding.md)|カスタム バインドのセキュリティ オプションを指定します。|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|セキュリティで保護されたメッセージ交換サービスの開始に使用される既定値を指定します。|  
  
## <a name="remarks"></a>解説  
 この設定は、サービスのセキュリティ ポリシーの一部として公開されず、クライアントのバインディングには影響を与えないため、ローカルです。  
  
 `localServiceSecuritySettings` 要素の以下の属性は、サービス拒否 (DOS) セキュリティ攻撃を軽減するために役立ちます。  
  
- `maxCachedCookies`: SPNEGO または SSL の各ネゴシエーションの実行後にサーバーによってキャッシュされる、期限付きの SecurityContextTokens の最大数を制御します。  
  
- `issuedCookieLifetime`: SPNEGO または SSL の各ネゴシエーションに続いてサーバーが発行する SecurityContextTokens の有効期限を制御します。 サーバーは、この期間だけ SecurityContextTokens をキャッシュします。  
  
- `maxPendingSessions`: サーバーで確立されているが、そのアプリケーション メッセージが処理されていない、セキュリティで保護されたメッセージ交換の最大数を制御します。 このクォータは、クライアントが、セキュリティで保護されたメッセージ交換をサービスで確立しないようにします。それによって、サービスはクライアントごとの状態を保持できますが、それらの状態を使用することはありません。  
  
- `inactivityTimeout`: サービスが、セキュリティで保護されたメッセージ交換を、それに対するアプリケーション メッセージを受信しなくても維持する最長時間を制御します。 このクォータは、クライアントが、セキュリティで保護されたメッセージ交換をサービスで確立しないようにします。それによって、サービスはクライアントごとの状態を保持できますが、それらの状態を使用することはありません。  
  
 セキュリティで保護されたメッセージ交換セッションでは、バインディングの `inactivityTimeout` 属性および `receiveTimeout` 属性の両方が、セッション タイムアウトに影響します。 2 つのうち短い方が、タイムアウトが発生する時間を決定します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalServiceSettings%2A>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A>
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [方法: SecurityBindingElement を使用してカスタム バインドを作成する](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [カスタム バインディング セキュリティ](../../../wcf/samples/custom-binding-security.md)
