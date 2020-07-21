---
ms.openlocfilehash: ed526095459a48aa37b585dfed79cc12b9fb9e56
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622046"
---
### <a name="some-net-apis-cause-first-chance-handled-entrypointnotfoundexceptions"></a>一部の .NET API がファースト チャンス (処理済み) EntryPointNotFoundExceptions の原因になります

#### <a name="details"></a>説明

.NET Framework 4.5 では、少数の .NET メソッドが、ファースト チャンス <xref:System.EntryPointNotFoundException?displayProperty=fullName> をスローするようになりました。 これらの例外は .NET Framework 内で処理されますが、ファースト チャンス例外を予期していないテスト自動化を中断することがありました。 これらと同じ API は、HighVersionLie が有効なとき、一部の ApiVerifier シナリオを中断させます。

#### <a name="suggestion"></a>提案される解決策

このバグは、.NET Framework 4.5.1 にアップグレードすることによって回避できます。 または、ファースト チャンス <xref:System.EntryPointNotFoundException?displayProperty=fullName> で中断しないように、テスト自動化を更新できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String,System.String,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.%23ctor(System.Type)></li></ul>|
