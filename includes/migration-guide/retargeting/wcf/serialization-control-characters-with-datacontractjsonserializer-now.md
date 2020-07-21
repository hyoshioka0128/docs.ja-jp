---
ms.openlocfilehash: afdf1e20db7dc564ddfb6028238604f97e00971a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614793"
---
### <a name="serialization-of-control-characters-with-datacontractjsonserializer-is-now-compatible-with-ecmascript-v6-and-v8"></a>DataContractJsonSerializer による制御文字のシリアル化が ECMAScript V6 および V8 対応に

#### <a name="details"></a>説明

.NET framework 4.6.2 以前のバージョンでは、<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> で、ECMAScript V6 および V8 標準と互換性がある方法で \b、\f、\t などの一部の特殊制御文字がシリアル化されませんでした。 .NET Framework 4.7 以降、これらの制御文字のシリアル化は ECMAScript V6 および V8 と互換性があります。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7 を対象とするアプリの場合、この機能は既定で有効になっています。 この動作が望ましくない場合は、app.config または web.config ファイルの `<runtime>` セクションに次の行を追加して、この機能を無効にすることができます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseECMAScriptV6EscapeControlCharacter=false" />
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject(System.Xml.XmlDictionaryWriter,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject(System.Xml.XmlWriter,System.Object)?displayProperty=nameWithType>
