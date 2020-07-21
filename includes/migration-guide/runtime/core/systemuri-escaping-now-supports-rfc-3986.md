---
ms.openlocfilehash: 1d7dc808d5b514acc582675d6ccdbd5778314624
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620265"
---
### <a name="systemuri-escaping-now-supports-rfc-3986"></a>System.Uri エスケープで RFC 3986 がサポート対象に

#### <a name="details"></a>説明

URI エスケープは、.NET Framework 4.5 で、[RFC 3986](https://tools.ietf.org/html/rfc3986) をサポートするように変更されました。 具体的な変更内容:<ul><li><xref:System.Uri.EscapeDataString(System.String)?displayProperty=fullName> は、予約されている文字を RFC 3986 に基づいてエスケープします。</li><li><xref:System.Uri.EscapeUriString(System.String)?displayProperty=fullName> は、予約されている文字をエスケープしません。</li><li><xref:System.Uri.UnescapeDataString(System.String)?displayProperty=fullName> は、無効なエスケープ シーケンスが発生した場合に例外をスローしません。</li><li>予約されていないエスケープ文字はエスケープ解除されます。</li></ul>

#### <a name="suggestion"></a>提案される解決策

<ul><li>無効なエスケープ シーケンスの場合、<xref:System.Uri.UnescapeDataString(System.String)?displayProperty=fullName> のスローに依存しないように、アプリケーションを更新します。 このようなシーケンスは、直接削除する必要があります。</li><li>同様に、エスケープおよびエスケープ解除された URI とデータ文字列は、.NET Framework 4.0 と .NET Framework 4.5 で異なる場合があるため、.NET のバージョン間で直接比較しないでください。 代わりに、1 つの .NET バージョンで解析と正規化を行ってから比較してください。</li></ul>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Uri.EscapeDataString(System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.EscapeUriString(System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.UnescapeDataString(System.String)?displayProperty=nameWithType></li></ul>|
