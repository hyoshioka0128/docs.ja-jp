---
title: '方法: 時刻のずれの最大値を設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- MaxClockSkew property
- WCF, custom bindings
ms.assetid: 491d1705-eb29-43c2-a44c-c0cf996f74eb
ms.openlocfilehash: f8231acade6821c95a76a608633fe443f4add8ab
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84586917"
---
# <a name="how-to-set-a-max-clock-skew"></a>方法: 時刻のずれの最大値を設定する
時刻が重要な要素となる機能は、2 台のコンピューターで時刻の設定が異なっていると失敗する可能性があります。 この可能性を減らすには、`MaxClockSkew` プロパティを <xref:System.TimeSpan> に設定します。 このプロパティは、次の 2 つのクラスで使用できます。  
  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>  
  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>  
  
> [!IMPORTANT]
> セキュリティで保護された通信を行うには、サービスまたはクライアントをブートストラップするときに、プロパティに対する変更を `MaxClockSkew` 行う必要があります。 これを行うには、 <xref:System.ServiceModel.Channels.SecurityBindingElement> プロパティによって返されるのプロパティを設定する必要があり <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.BootstrapSecurityBindingElement%2A?displayProperty=nameWithType> ます。  
  
 システム提供のバインディングの 1 つでこのプロパティを変更するには、バインディングのコレクションでセキュリティ バインド要素を見つけて、`MaxClockSkew` プロパティを新しい値に設定する必要があります。 <xref:System.ServiceModel.Channels.SecurityBindingElement> から派生される 2 つのクラスは、<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> クラスおよび <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> クラスです。 コレクションからセキュリティ バインディングを取得する場合は、`MaxClockSkew` プロパティを正しく設定するために、これらの型のどちらかにキャストする必要があります。 次の例では、<xref:System.ServiceModel.WSHttpBinding> を使用していますが、これは <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> を使用します。 システム指定の各バインディングで使用するセキュリティバインディングの種類を指定する一覧については、「[システム指定](../system-provided-bindings.md)のバインディング」を参照してください。  
  
## <a name="to-create-a-custom-binding-with-a-new-clock-skew-value-in-code"></a>コードを使用して時刻のずれの新しい値を持つカスタム バインドを作成するには  
  
> [!WARNING]
> コード内の次の名前空間への参照を追加します。 <xref:System.ServiceModel.Channels> 、、 <xref:System.ServiceModel.Description> <xref:System.Security.Permissions> 、および <xref:System.ServiceModel.Security.Tokens> 。  
  
1. <xref:System.ServiceModel.WSHttpBinding> クラスのインスタンスを作成し、セキュリティ モードを <xref:System.ServiceModel.SecurityMode.Message?displayProperty=nameWithType> に設定します。  
  
2. <xref:System.ServiceModel.Channels.BindingElementCollection> メソッドを呼び出して、<xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A> クラスの新しいインスタンスを作成します。  
  
3. <xref:System.ServiceModel.Channels.BindingElementCollection.Find%2A> クラスの <xref:System.ServiceModel.Channels.BindingElementCollection> メソッドを使用して、セキュリティ バインド要素を検索します。  
  
4. <xref:System.ServiceModel.Channels.BindingElementCollection.Find%2A> メソッドを使用する場合には、実際の型にキャストします。 次の例では <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 型にキャストしています。  
  
5. セキュリティ バインド要素の <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A> プロパティを設定します。  
  
6. 適切なサービス型とベース アドレスを使用して、<xref:System.ServiceModel.ServiceHost> を作成します。  
  
7. <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> メソッドを使用してエンドポイントを追加し、<xref:System.ServiceModel.Channels.CustomBinding> を含めます。  
  
     [!code-csharp[c_MaxClockSkew#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_maxclockskew/cs/source.cs#1)]
     [!code-vb[c_MaxClockSkew#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_maxclockskew/vb/source.vb#1)]  
  
## <a name="to-set-the-maxclockskew-in-configuration"></a>構成で MaxClockSkew を設定するには  
  
1. [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md)要素セクションでを作成し [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md) ます。  
  
2. 要素を作成 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) し、 `name` 属性を適切な値に設定します。 `MaxClockSkewBinding` に設定する方法の例を次に示します。  
  
3. エンコーディング要素を追加します。 次の例では、を追加し [\<textMessageEncoding>](../../configure-apps/file-schema/wcf/textmessageencoding.md) ます。  
  
4. 要素を追加 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) し、属性を `authenticationMode` 適切な設定に設定します。 次の例では、この属性を `Kerberos` に設定して、サービスが Windows 認証を使用するように指定しています。  
  
5. を追加 [\<localServiceSettings>](../../configure-apps/file-schema/wcf/localservicesettings-element.md) し、 `maxClockSkew` 属性をの形式の値に設定し `"##:##:##"` ます。 次の例では 7 分に設定しています。 必要に応じて、を追加 [\<localServiceSettings>](../../configure-apps/file-schema/wcf/localservicesettings-element.md) し、 `maxClockSkew` 属性を適切な設定に設定します。  
  
6. transport 要素を追加します。 次の例では、を使用 [\<httpTransport>](../../configure-apps/file-schema/wcf/httptransport.md) します。  
  
7. セキュリティで保護された通信を行うには、要素のブートストラップでセキュリティ設定を行う必要があり [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) ます。  
  
    ```xml  
    <bindings>  
      <customBinding>  
        <binding name="MaxClockSkewBinding">  
            <textMessageEncoding />  
            <security authenticationMode="Kerberos">  
               <localClientSettings maxClockSkew="00:07:00" />  
               <localServiceSettings maxClockSkew="00:07:00" />  
               <secureConversationBootstrap>  
                  <localClientSettings maxClockSkew="00:30:00" />  
                  <localServiceSettings maxClockSkew="00:30:00" />  
               </secureConversationBootstrap>  
            </security>  
            <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [方法: SecurityBindingElement を使用してカスタム バインドを作成する](how-to-create-a-custom-binding-using-the-securitybindingelement.md)
