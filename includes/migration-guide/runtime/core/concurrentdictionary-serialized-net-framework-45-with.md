---
ms.openlocfilehash: ae0f68a19d6eae53998d61e924cfef3aaaec1784
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620230"
---
### <a name="a-concurrentdictionary-serialized-in-net-framework-45-with-netdatacontractserializer-cannot-be-deserialized-by-net-framework-451-or-452"></a>NetDataContractSerializer を使用して .NET Framework 4.5 でシリアル化された ConcurrentDictionary は、.NET Framework 4.5.1 または 4.5.2 で逆シリアル化できない

#### <a name="details"></a>説明

型に対する内部的な変更のため、<xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName> を使って .NET Framework 4.5 でシリアル化された <xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクトは、.NET Framework 4.5.1 または .NET Framework 4.5.2 では逆シリアル化できません。反対の方向 (.NET Framework 4.5.x でシリアル化して、.NET Framework 4.5 で逆シリアル化する) は動作することに注意してください。 同様に、すべての 4.x バージョン間のシリアル化は、.NET Framework 4.6 で機能します。 .NET Framework の 1 つのバージョンでのシリアル化と逆シリアル化は影響を受けません。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.5 と .NET Framework 4.5.1/4.5.2 の間で <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> のシリアル化と逆シリアル化を行う必要がある場合は、<xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName> の代わりに、<xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> または <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName> シリアライザーなど、代替のシリアライザーを使う必要があります。または、この問題は .NET Framework 4.6 で修正されたため、このバージョンの .NET Framework にアップグレードすることによって解決できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5.1|
|種類|ランタイム|
