---
title: フェデレーションと信頼
ms.date: 03/30/2017
helpviewer_keywords:
- federation [WCF], and trust
ms.assetid: 4bdec4f2-f8a2-4512-bdcf-14ef54b5877a
ms.openlocfilehash: 8b924a4aeb9c667592e99d65666cd8f048d34c22
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595480"
---
# <a name="federation-and-trust"></a>フェデレーションと信頼
このトピックでは、Windows Communication Foundation (WCF) でのフェデレーションアプリケーション、信頼の境界と構成、および発行済みトークンの使用に関連するさまざまな側面について説明します。  
  
## <a name="services-security-token-services-and-trust"></a>サービス、セキュリティ トークン サービス、および信頼  
 フェデレーション エンドポイントを公開するサービスを使用する場合、通常、特定の発行者によって提供されたトークンを使用してクライアント認証を行う必要があります。 そのため、発行者の正しい資格情報を使用してサービスが構成されていることが重要です。そうでないと、サービスは発行済みトークンの署名を検証することができず、クライアントはサービスと通信できません。 サービスで発行者の資格情報を構成する方法の詳細については、「[方法: フェデレーションサービスで資格情報を構成する](how-to-configure-credentials-on-a-federation-service.md)」を参照してください。  
  
 同様に、対称キーを使用する場合も、キーがターゲット サービス用に暗号化されるため、セキュリティ トークン サービスがターゲット サービスの正しい資格情報で構成される必要があります。そうでないと、セキュリティ トークン サービスはターゲット サービス用にキーを暗号化できないため、この場合も、クライアントはサービスと通信できなくなります。  
  
 WCF サービスは、のプロパティの値を使用して、 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A> クライアントとサービスの間のクロックスキューを可能にします。 [SecurityBindingElement](../diagnostics/wmi/securitybindingelement.md) フェデレーションでは、`MaxClockSkew` 設定が、クライアントと、クライアントが発行済みトークンを取得したセキュリティ トークン サービスの両方の時刻のずれに対して適用されます。 そのため、発行済みトークンの有効期間の開始時刻と終了時刻が設定する際、セキュリティ トークン サービスで時刻のずれを許可する必要はありません。  
  
> [!NOTE]
> 時刻のずれの重要性は、発行済みトークンの有効期間が短くなるほど大きくなります。 トークンの有効期間が 30 分以上あれば、多くの場合、時刻のずれは大きな問題にはなりません。 短い有効期間が使用されるシナリオやトークンの正確な有効時間が重要となるシナリオでは、時刻のずれを考慮に入れて設計する必要があります。  
  
## <a name="federated-endpoints-and-time-outs"></a>フェデレーション エンドポイントとタイムアウト  
 クライアントがフェデレーション エンドポイントと通信するときは、最初にセキュリティ トークン サービスから適切なトークンを取得する必要があります。 このセキュリティ トークン サービスがフェデレーション エンドポイントを公開している場合、クライアントは最初にそのエンドポイントの発行者からトークンを取得する必要があります。 それぞれのトークンの取得には時間がかかり、この時間が実際のメッセージを最終的なエンドポイントに送信するときの全体的なタイムアウトの影響を受けます。  
  
 たとえば、クライアント側チャネルのタイムアウトが 30 秒に設定されているとします。 またメッセージを最終的なエンドポイントに送信する前に、トークンを取得するために 2 つのトークン発行者を呼び出す必要があり、それぞれのトークンの発行に 15 秒を要するとします。 この場合、この試行は失敗し、<xref:System.TimeoutException> がスローされます。 したがって、クライアント チャネルの <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> 値は、すべての発行済みトークンを取得するのにかかる時間を含めた、十分大きな値に設定する必要があります。 <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> プロパティの値が指定されていない場合、<xref:System.ServiceModel.Channels.Binding.OpenTimeout%2A> プロパティ、または <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A> プロパティ (あるいはその両方) を、すべての発行済みトークンを取得するのにかかる時間を含めた、十分大きな値に設定する必要があります。  
  
## <a name="token-lifetime-and-renewal"></a>トークンの有効期間と更新  
 WCF クライアントは、サービスへの初期要求を行うときに、発行されたトークンを確認しません。  代わりに、WCF は Security Token Service を信頼して、適切な有効期間と有効期限があるトークンを発行します。 トークンがクライアントによってキャッシュされて再使用される場合は、トークンの有効期間が、後続する要求によってチェックされ、クライアントは必要に応じてトークンを自動的に更新します。 トークンキャッシュの詳細については、「[方法: フェデレーションクライアントを作成](how-to-create-a-federated-client.md)する」を参照してください。  
  
 短い有効期間を指定すると、発行されるトークンまたはセキュリティコンテキストトークンに対して30秒以下の順序で、発行されたトークンを要求するとき、またはセキュリティコンテキストトークンをネゴシエートまたは更新するときに、WCF クライアントによってネゴシエーションのタイムアウトまたは他の例外がスローされる可能性があります。  
  
## <a name="issued-tokens-and-inclusionmode"></a>発行済みトークンと InclusionMode  
 クライアントからフェデレーション エンドポイントに送信されたメッセージで発行済みトークンがシリアル化されるかどうかは、<xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.InclusionMode%2A> クラスの <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters> プロパティを設定することによって制御します。 このプロパティは <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode> 列挙値のいずれかに設定できますが、これはほとんどのフェデレーション シナリオでは役に立ちません。 `SecurityTokenInclusionMode.Never` 値および `SecurityTokenInclusionMode.AlwaysToInitiator` 値を設定すると、クライアントによって、セキュリティ トークンサービスによって発行されたトークンへの参照が証明書利用者に送信されます。 証明書利用者がこの発行済みトークンのコピーを持っていない限り、トークン参照が解決されないため、認証は失敗します。 WCF `SecurityTokenInclusionMode.Once` はと同等として扱い `SecurityTokenInclusionMode.AlwaysToRecipient` ます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>
- [方法: フェデレーション クライアントを作成する](how-to-create-a-federated-client.md)
- [方法: フェデレーション サービスで資格情報を設定する](how-to-configure-credentials-on-a-federation-service.md)
- [方法: WSFederationHttpBinding を作成する](how-to-create-a-wsfederationhttpbinding.md)
