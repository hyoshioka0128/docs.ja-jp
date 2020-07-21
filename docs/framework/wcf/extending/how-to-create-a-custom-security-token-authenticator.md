---
title: '方法 : カスタム セキュリティ トークン認証システムを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, authentication
ms.assetid: 10e245f7-d31e-42e7-82a2-d5780325d372
ms.openlocfilehash: 7bbe59958f59f76046c0a112463cfa64d09c14d3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185589"
---
# <a name="how-to-create-a-custom-security-token-authenticator"></a>方法 : カスタム セキュリティ トークン認証システムを作成する
ここでは、カスタム セキュリティ トークン認証システムの作成方法と、これをカスタム セキュリティ トークン マネージャーに統合する方法を示します。 セキュリティ トークン認証システムは受信メッセージと共に提出されるセキュリティ トークンの内容を検証します。 検証に成功すると、認証システムは <xref:System.IdentityModel.Policy.IAuthorizationPolicy> インスタンスのコレクションを返します。これが評価されるとクレーム セットが返されます。  
  
 Windows 通信基盤 (WCF) でカスタム セキュリティ トークン認証を使用するには、最初にカスタム資格情報とセキュリティ トークン マネージャーの実装を作成する必要があります。 カスタム資格情報とセキュリティ トークン マネージャーの作成の詳細については、「[チュートリアル: カスタム クライアント資格情報とサービス資格情報の作成](walkthrough-creating-custom-client-and-service-credentials.md)」を参照してください。
  
## <a name="procedures"></a>手順  
  
#### <a name="to-create-a-custom-security-token-authenticator"></a>カスタム セキュリティ トークン認証システムを作成するには  
  
1. <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> クラスから派生する新しいクラスを定義します。  
  
2. <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.CanValidateTokenCore%2A> メソッドをオーバーライドします。 カスタム認証システムが受信トークンの種類を検証できるかどうかによって、メソッドから `true` または `false` が返されます。  
  
3. <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.ValidateTokenCore%2A> メソッドをオーバーライドします。 このメソッドでは、トークンの内容を適切に検証する必要があります。 トークンが検証手順をパスすると、<xref:System.IdentityModel.Policy.IAuthorizationPolicy> インスタンスのコレクションが返されます。 下記の例では、次の手順で作成するカスタム承認ポリシーの実装を使用します。  
  
     [!code-csharp[C_CustomTokenAuthenticator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#1)]
     [!code-vb[C_CustomTokenAuthenticator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#1)]  
  
 上記のコードでは、<xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.CanValidateToken%28System.IdentityModel.Tokens.SecurityToken%29> メソッドに承認ポリシーのコレクションが返されます。 WCF では、このインターフェイスのパブリック実装は提供されません。 以下の手順では、これを独自の要件について実行する方法を示します。  
  
#### <a name="to-create-a-custom-authorization-policy"></a>カスタム承認ポリシーを作成するには  
  
1. <xref:System.IdentityModel.Policy.IAuthorizationPolicy> インターフェイスを実装する新しいクラスを定義します。  
  
2. <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> の読み取り専用プロパティを実装します。 このプロパティを実装する方法の 1 つは、クラスのコンストラクターでグローバル一意識別子 (GUID) を生成し、この値をプロパティの値が求められるたびに返すことです。  
  
3. <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A> の読み取り専用プロパティを実装します。 このプロパティは、トークンから取得されるクレーム セットの発行者を返す必要があります。 この発行者は、トークンの発行者、またはトークンの内容を検証する証明機関に対応している必要があります。 次の例では、前の手順で作成したカスタム セキュリティ トークン認証システムから、このクラスに渡された発行者クレームを使用します。 カスタム セキュリティ トークン認証システムでは、(<xref:System.IdentityModel.Claims.ClaimSet.System%2A> プロパティから返される) システム提供のクレーム セットを使用して、ユーザー名トークンの発行者を表します。  
  
4. <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> メソッドを実装します。 このメソッドは (引数として渡される) <xref:System.IdentityModel.Policy.EvaluationContext> クラスのインスタンスに、受信セキュリティ トークンの内容に基づいたクレームを設定します。 評価が完了したら、メソッドは `true` を返します。 実装が、評価コンテキストに追加情報を提供する他の承認ポリシーの存在に依存している場合、必要な情報が評価コンテキスト内に存在していないと、このメソッドは `false` を返します。 その場合、WCF は、少なくとも 1 つの承認ポリシーが評価コンテキストを変更した場合、受信メッセージに対して生成された他のすべての承認ポリシーを評価した後、メソッドを再度呼び出します。  
  
     [!code-csharp[c_CustomTokenAuthenticator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#3)]
     [!code-vb[c_CustomTokenAuthenticator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#3)]  

 [チュートリアル: カスタム クライアント資格情報とサービス資格情報の作成](walkthrough-creating-custom-client-and-service-credentials.md)では、カスタム資格情報とカスタム セキュリティ トークン マネージャーを作成する方法について説明します。 ここで作成したカスタム セキュリティ トークン認証システムを使用するには、<xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A> メソッドからカスタム認証システムを返すようにセキュリティ トークン マネージャーの実装を変更します。 適切なセキュリティ トークン要件が渡されると、このメソッドは認証システムを返します。  
  
#### <a name="to-integrate-a-custom-security-token-authenticator-with-a-custom-security-token-manager"></a>カスタム セキュリティ トークン マネージャーにカスタム セキュリティ トークン認証システムを統合するには  
  
1. カスタム セキュリティ トークン マネージャーの実装の <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A> メソッドをオーバーライドします。  
  
2. <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> パラメーターに基づいてカスタム セキュリティ トークン認証システムを返すロジックをメソッドに追加します。 次の例では、トークン要件のトークンの種類が (<xref:System.IdentityModel.Tokens.SecurityTokenTypes.UserName%2A> プロパティで表される) ユーザー名で、セキュリティ トークン認証システムで要求されているメッセージの方向 (<xref:System.ServiceModel.Description.MessageDirection.Input> フィールドで表される) が入力である場合、カスタム セキュリティ トークン認証システムが返されます。  
  
     [!code-csharp[c_CustomTokenAuthenticator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#2)]
     [!code-vb[c_CustomTokenAuthenticator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#2)]  

## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.IdentityModel.Tokens.UserNameSecurityToken>
- [チュートリアル: カスタム クライアントおよびサービスの資格情報を作成する](walkthrough-creating-custom-client-and-service-credentials.md)
- [方法 : カスタム セキュリティ トークン プロバイダーを作成する](how-to-create-a-custom-security-token-provider.md)
