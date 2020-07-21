---
ms.openlocfilehash: 57f68c10d5d1edc9b8deaca2f4fe7edda2dd69b0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620395"
---
### <a name="systemservicemodelwebwebservicehost-object-no-longer-adds-a-default-endpoint"></a>System.ServiceModel.Web.WebServiceHost オブジェクトは、既定のエンドポイントを追加しなくなりました

#### <a name="details"></a>説明

<xref:System.ServiceModel.Web.WebServiceHost> オブジェクトでは、アプリケーション コードによって明示的なエンドポイントが追加された場合に、既定のエンドポイントが追加されなくなりました。

#### <a name="suggestion"></a>提案される解決策

ユーザーが既定のエンドポイントに接続できることを期待していて、他の明示的なエンドポイントが <xref:System.ServiceModel.Web.WebServiceHost?displayProperty=fullName> に追加されている場合は、既定のエンドポイントも明示的に追加する必要があります (<xref:System.ServiceModel.ServiceHostBase.AddDefaultEndpoints?displayProperty=fullName> を使用して)。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.ServiceModel.ServiceHost.AddServiceEndpoint(System.Type,System.ServiceModel.Channels.Binding,System.String)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHost.AddServiceEndpoint(System.Type,System.ServiceModel.Channels.Binding,System.Uri)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHost.AddServiceEndpoint(System.Type,System.ServiceModel.Channels.Binding,System.String,System.Uri)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHost.AddServiceEndpoint(System.Type,System.ServiceModel.Channels.Binding,System.Uri,System.Uri)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHost.AddServiceEndpoint(System.Type,System.ServiceModel.Channels.Binding,System.Uri,System.Uri)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint(System.ServiceModel.Description.ServiceEndpoint)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint(System.String,System.ServiceModel.Channels.Binding,System.String)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint(System.String,System.ServiceModel.Channels.Binding,System.Uri)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint(System.String,System.ServiceModel.Channels.Binding,System.String,System.Uri)?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint(System.String,System.ServiceModel.Channels.Binding,System.Uri,System.Uri)?displayProperty=nameWithType></li></ul>|
