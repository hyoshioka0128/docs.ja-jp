---
ms.openlocfilehash: 5a3370e71488e4f9d8d933b504d1d771c78e0385
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620380"
---
### <a name="soapformatter-cannot-deserialize-hashtable-and-similar-ordered-collection-objects"></a>SoapFormatter は、ハッシュテーブルなどの順序付けられたコレクション オブジェクトを逆シリアル化できない

#### <a name="details"></a>説明

<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter?displayProperty=fullName> は、特定のバージョンの .NET Framework でシリアル化されたオブジェクトが別のバージョンで正常に逆シリアル化されることを保証しません。 具体的には、(<xref:System.Collections.Hashtable?displayProperty=fullName> のような) 順序付けられたコレクションの中には、4.0 と 4.5 の間でメンバーが追加されたものがあり、このような種類のオブジェクトが .NET Framework 4.5 でシリアル化された場合、.NET Framework 4.0 では逆シリアル化できません。 シリアル化データのシリアル化と逆シリアル化の両方が同じバージョンの .NET Framework で行われた場合、問題は発生しないことに注意してください。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter?displayProperty=fullName> のシリアル化は、.NET Framework の変更に対応できる <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName> のシリアル化または <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName> に置き換える必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Serialize(System.IO.Stream,System.Object,System.Runtime.Remoting.Messaging.Header[])?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Deserialize(System.IO.Stream,System.Runtime.Remoting.Messaging.HeaderHandler)?displayProperty=nameWithType></li></ul>|
