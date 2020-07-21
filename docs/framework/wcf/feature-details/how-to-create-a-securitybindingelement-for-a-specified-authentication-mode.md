---
title: '方法: 指定した認証モード用の SecurityBindingElement を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a7c7747a-5b8c-463f-8493-7266dac75066
ms.openlocfilehash: 9aebe6d8cc82c454161daead49b55f02a1cca4a7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598945"
---
# <a name="how-to-create-a-securitybindingelement-for-a-specified-authentication-mode"></a>方法: 指定した認証モード用の SecurityBindingElement を作成する
Windows Communication Foundation (WCF) では、クライアントとサービスが相互に認証するために使用されるモードがいくつかあります。 これらの認証モード用のセキュリティ バインド要素は、次の例のように、<xref:System.ServiceModel.Channels.SecurityBindingElement> クラスの静的メソッドまたは構成を使用して作成できます。  
  
 18認証モードの詳細については、「[認証モードの認証](securitybindingelement-authentication-modes.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、複数の認証モードのバインディングを作成するメソッドを示します。  
  
> [!NOTE]
> <xref:System.ServiceModel.Channels.SecurityBindingElement> オブジェクトのインスタンスが一度作成されると、<xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.KeyType%2A> や <xref:System.ServiceModel.Channels.SecurityBindingElement.MessageSecurityVersion%2A> などの多数のプロパティは変更できなくなります。 これらのプロパティで `set` を呼び出しても変更されません。  
  
 [!code-csharp[c_CustomBindingsAuthMode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombindingsauthmode/cs/source.cs#2)]
 [!code-vb[c_CustomBindingsAuthMode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombindingsauthmode/vb/source.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [SecurityBindingElement 認証モード](securitybindingelement-authentication-modes.md)
- [方法: SecurityBindingElement を使用してカスタム バインドを作成する](how-to-create-a-custom-binding-using-the-securitybindingelement.md)
