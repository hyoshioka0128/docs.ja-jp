---
title: 認証のためのサービスの ID のオーバーライド
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d613a22b-07d7-41a4-bada-1adc653b9b5d
ms.openlocfilehash: 5649ef4cc05c9c16b1f8f626ba5e2e584b0e52eb
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278913"
---
# <a name="override-the-identity-of-a-service-for-authentication"></a>認証用のサービスの ID をオーバーライドする

クライアント資格情報の種類を選択すると、サービス メタデータで公開される ID の種類が指定されるため、通常、サービスで ID を設定する必要はありません。 たとえば、次の構成コードでは[\<、wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)要素を使用し`clientCredentialType`、属性を Windows に設定します。  

 次の Web サービス記述言語 (WSDL) コードは、定義済みのエンドポイントの ID を示しています。 この例では、サービスが特定のユーザー アカウント (username@contoso.com) で自己ホスト型サービスとして実行されているため、ユーザー プリンシパル名 (UPN) ID にはアカウント名が含まれています。 UPN は、Windows ドメインのユーザー サインイン名とも呼ばれます。  

 ID 設定を示すサンプル アプリケーションについては、「[サービス ID](../samples/service-identity-sample.md)のサンプル」を参照してください。 サービス ID の詳細については、「[サービス ID と認証](../feature-details/service-identity-and-authentication.md)」を参照してください。  
  
## <a name="kerberos-authentication-and-identity"></a>Kerberos 認証と ID  
 既定では、サービスが Windows 資格情報を使用するように構成されている場合、[\<ユーザー プリンシパル名>](../../configure-apps/file-schema/wcf/userprincipalname.md)または[\<サービス プリンシパル名>](../../configure-apps/file-schema/wcf/serviceprincipalname.md)要素を含む[\<id>](../../configure-apps/file-schema/wcf/identity.md)要素が WSDL 内に生成されます。 `LocalSystem`サービスが 、`LocalService`または`NetworkService`アカウントで実行されている場合、サービス プリンシパル名 (SPN) は、既定では`host/`\<*ホスト名*>の形式で生成されます。 サービスが別のアカウントで実行されている場合は、Windows 通信基盤 (WCF) は\<*、ユーザー名*>@<*ドメイン名*`>`の形式で UPN を生成します。 これらが生成されるのは、Kerberos 認証では、サービスを認証するために UPN または SPN をクライアントに提供する必要があるからです。  
  
 また[、Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731241(v=ws.10)?redirectedfrom=MSDN)ツールを使用して、ドメイン内のサービスのアカウントに追加の SPN を登録することもできます。 登録した SPN は、そのサービスの ID として使用できます。 このツールの詳細については、「 [Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc773257(v=ws.10))の概要 」を参照してください。  
  
> [!NOTE]
> ネゴシエーションを行わずに Windows 資格情報を使用するには、サービスのユーザー アカウントが Active Directory ドメインに登録された SPN にアクセスできる必要があります。 これは、次の方法で行うことができます。  
  
- サービスを実行するには、NetworkService アカウントまたは LocalSystem アカウントを使用します。 これらのアカウントは、コンピューターが Active Directory ドメインに参加するときに確立されるコンピューター SPN にアクセスできるため、WCF はサービスのメタデータ (WSDL) 内のサービスのエンドポイント内で適切な SPN 要素を自動的に生成します。  
  
- 任意の Active Directory ドメイン アカウントを使用してサービスを実行します。 この場合、そのドメイン アカウント用の SPN を確立します。これには、Setspn.exe ユーティリティ ツールを使用できます。 サービスのアカウントの SPN を作成したら、その SPN をそのメタデータ (WSDL) を通じてサービスのクライアントに発行するように WCF を構成します。 これを行うには、アプリケーション構成ファイルまたはコードを使用して、公開されるエンドポイントのエンドポイント ID を設定します。  
  
 SPN、Kerberos プロトコル、およびアクティブ ディレクトリの詳細については[、「Windows 用 Kerberos テクニカル サプリメント](https://docs.microsoft.com/previous-versions/msp-n-p/ff649429(v=pandp.10))」を参照してください。  
  
### <a name="when-spn-or-upn-equals-the-empty-string"></a>SPN または UPN が空の文字列の場合  
 空の文字列の SPN または UPN を設定した場合は、使用しているセキュリティ レベルと認証モードに応じて、次のようになります。  
  
- トランスポート レベルのセキュリティを使用している場合は、NTLM (NT LanMan) 認証が選択されます。  
  
- メッセージ レベルのセキュリティを使用している場合は、認証モードによっては認証に失敗する可能性があります。  
  
- mode を使用`spnego`していて、属性`AllowNtlm`が に`false`設定されている場合、認証は失敗します。  
  
- mode を使用`spnego`していて、`AllowNtlm`属性が に`true`設定されている場合、UPN が空の場合は認証は失敗しますが、SPN が空の場合は成功します。  
  
- Kerberos ダイレクト ("ワンショット" とも呼ばれます) を使用している場合は、認証に失敗します。  
  
### <a name="use-the-identity-element-in-configuration"></a>構成で\<要素> ID を使用する  
 前に示したバインディングでクライアント資格情報の種類を`Certificate`変更すると、生成された WSDL には、次のコードに示すように、ID 値の Base64 シリアル化された X.509 証明書が含まれます。 これは、Windows 以外のすべてのクライアント資格情報の種類の既定値です。  

 既定のサービス ID の値を変更したり、構成で <`identity`> 要素を使用するか、コードで ID を設定することによって、ID の種類を変更したりできます。 値 `contoso.com` を使用してドメイン ネーム システム (DNS) ID を設定する構成コードを次に示します。  

### <a name="set-identity-programmatically"></a>プログラムで ID を設定する  
 WCF によって自動的に決定されるため、サービスは ID を明示的に指定する必要はありません。 ただし、WCF では、必要に応じてエンドポイントで ID を指定できます。 特定の DNS ID を持つ新しいサービス エンドポイントを追加するコードを次に示します。  
  
 [!code-csharp[C_Identity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_identity/cs/source.cs#5)]
 [!code-vb[C_Identity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_identity/vb/source.vb#5)]  
  
## <a name="see-also"></a>関連項目

- [方法: カスタム クライアント ID 検証機能を作成する](how-to-create-a-custom-client-identity-verifier.md)
- [サービス ID と認証](../feature-details/service-identity-and-authentication.md)
