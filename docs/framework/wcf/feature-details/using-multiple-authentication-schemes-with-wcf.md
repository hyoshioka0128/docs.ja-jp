---
title: WCF での複数の認証方式の使用
ms.date: 03/30/2017
ms.assetid: f32a56a0-e2b2-46bf-a302-29e1275917f9
ms.openlocfilehash: 1874963573a6ec12939bd12b79574f1e2c889bfd
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600219"
---
# <a name="using-multiple-authentication-schemes-with-wcf"></a>WCF での複数の認証方式の使用
WCF では、単一のエンドポイントに複数の認証方式を指定できるようになりました。 さらに、Web ホスト サービスは、認証設定を IIS から直接継承できます。 自己ホスト型サービスは、使用可能な認証方式を指定できます。 IIS での認証設定の詳細については、「 [Iis 認証](https://go.microsoft.com/fwlink/?LinkId=232458)」を参照してください。  
  
## <a name="iis-hosted-services"></a>IIS でホストされるサービス  
 IIS でホストされるサービスでは、IIS で使用する認証方式を設定します。 次の XML スニペットに示すように、サービスの web.config ファイルのバインド構成で、clientCredential type を "InheritedFromHost" に指定します。  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 ServiceAuthenticationBehavior または要素を使用して、認証方式のサブセットのみをサービスで使用するように指定でき \<serviceAuthenticationManager> ます。 これをコードで構成する場合は、次のコード スニペットに示すように ServiceAuthenticationBehavior を使用します。  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
```  
  
 構成ファイルでこれを構成する場合は、 \<serviceAuthenticationManager> 次の XML スニペットに示すように要素を使用します。  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 この結果、IIS で選択した内容に応じて、ここに示されている認証方式のサブセットに限り、サービス エンドポイントへの適用が検討されます。 つまり、開発者は serviceAuthenticationManager の一覧から基本認証を省略することによって、リストから基本認証を除外することができます。IIS で有効になっている場合でも、サービス エンドポイントには適用されません。  
  
## <a name="self-hosted-services"></a>自己ホスト型サービス  
 自己ホスト型サービスは、設定を継承する IIS がないため、構成方法が少し異なります。 ここでは、 \<serviceAuthenticationManager> 要素または ServiceAuthenticationBehavior を使用して、継承される認証設定を指定します。 コード例を次に示します。  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
```  
  
 config では、次のようになります。  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 その後、次の XML スニペットに示すように、バインディング設定で InheritFromHost を指定できます。  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 または、次の構成スニペットに示すように、HTTP トランスポート バインド要素で認証方式を設定することにより、カスタム バインドで認証方式を指定することもできます。  
  
```xml  
<binding name="multipleBinding">  
      <textMessageEncoding/>  
      <httpTransport authenticationScheme="Negotiate, Ntlm, Digest, Basic" />  
    </binding>  
```  
  
## <a name="see-also"></a>関連項目

- [バインディングとセキュリティ](bindings-and-security.md)
- [エンドポイント:アドレス、バインディング、およびコントラクト](endpoints-addresses-bindings-and-contracts.md)
- [システムが提供するバインディングの構成](configuring-system-provided-bindings.md)
- [カスタム バインディングを使用したセキュリティ機能](security-capabilities-with-custom-bindings.md)
- [バインド](bindings.md)
- [カスタム バインディング](../extending/custom-bindings.md)
