---
title: '方法: Probe 要求の探索バージョンを特定する'
ms.date: 03/30/2017
ms.assetid: b3c4e2e2-2957-4074-ae6a-776a5ca84278
ms.openlocfilehash: 2b7e42714ae1d16a84bcb6f0fc79cf5b376a7a16
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595415"
---
# <a name="how-todetermine-the-discovery-version-of-a-probe-request"></a>方法: Probe 要求の探索バージョンを特定する

探索プロキシでは、異なる探索バージョンを使用する複数の探索エンドポイントを公開する場合があります。 UDP マルチキャストプローブ要求がプロキシに到着すると、プロキシはマルチキャスト抑制メッセージで応答する必要があります。 このためには、要求の探索バージョンを把握している必要があります。

## <a name="to-determine-the-discovery-version-of-a-probe-request"></a>Probe 要求の探索バージョンを特定するには

プローブ要求に応答するメソッド (たとえば) では、 <xref:System.ServiceModel.Discovery.DiscoveryProxy.OnBeginFind%2A?displayProperty=nameWithType> <xref:System.ServiceModel.OperationContext.Current%2A?displayProperty=nameWithType> 次のコードに示すように、静的プロパティを使用してを検索し <xref:System.ServiceModel.Discovery.DiscoveryOperationContextExtension> ます。

```csharp
DiscoveryOperationContextExtension doce = OperationContext.Current.Extensions.Find<DiscoveryOperationContextExtension>();
// Access the discovery version from the DiscoveryOperationContextExtension
doce.DiscoveryVersion;
```

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion%2A>
- [探索プロキシの実装](implementing-a-discovery-proxy.md)
