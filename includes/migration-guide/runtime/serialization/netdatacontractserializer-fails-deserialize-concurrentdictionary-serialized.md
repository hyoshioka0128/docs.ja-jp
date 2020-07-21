---
ms.openlocfilehash: eef5633ec8566f6d5216b7dca4387766cacb600d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620385"
---
### <a name="netdatacontractserializer-fails-to-deserialize-a-concurrentdictionary-serialized-with-a-different-net-version"></a>異なる .NET バージョンでシリアル化された ConcurrentDictionary を NetDataContractSerializer で逆シリアル化できない

#### <a name="details"></a>説明

設計上、<xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName> は、シリアル化と逆シリアル化の両方で、同一の CLR 型を共有する結果になる場合にのみ使用できます。 したがって、あるバージョンの .NET Framework でシリアル化されたオブジェクトを別のバージョンで逆シリアル化することは保証されません。<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> 型は、.NET Framework 4.5 以前でシリアル化された場合、.NET Framework 4.5.1 以降では正しく逆シリアル化されないことがわかっています。

#### <a name="suggestion"></a>提案される解決策

この問題の考えられるいくつかの回避策を以下に示します。<ul><li>シリアル化するコンピューターをアップグレードして、.NET Framework 4.5.1 も使用するようにします。</li><li>シリアル化と逆シリアル化の両方で CLT 型がまったく同じになることが想定されない場合は、<xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName> ではなく、<xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> を使用します。</li><li>この特定の 4.5-&gt;4.5.1 の問題は見られないため、<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> ではなく、<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> を使用します。</li></ul>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5.1|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Runtime.Serialization.NetDataContractSerializer.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li></ul>|
