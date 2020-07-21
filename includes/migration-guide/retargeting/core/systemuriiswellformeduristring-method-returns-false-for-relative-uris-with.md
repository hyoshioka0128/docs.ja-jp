---
ms.openlocfilehash: f7dcf9c4c3dc7ea536ddc847769a1a30f1298bb2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617213"
---
### <a name="systemuriiswellformeduristring-method-returns-false-for-relative-uris-with-a-colon-char-in-first-segment"></a>最初のセグメントにコロン文字を含む相対 URI に対して System.Uri.IsWellFormedUriString メソッドが false を返す

#### <a name="details"></a>説明

.NET Framework 4.5 より、<xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)> では、最初のセグメントに `:` を含む相対 URI が形式が正しくないとして処理されます。 これは .NET Framework 4.0 の <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=fullName> 動作からの変更であり、RFC3986 に準拠する目的で行われました。

#### <a name="suggestion"></a>提案される解決策

この変更は (他の多くの URI 変更と同様に) .NET Framework 4.5 (以降) を対象とするアプリケーションにのみ影響を与えます。 以前の動作を維持するには、アプリの対象を .NET Framework 4.0 にします。 あるいは、<xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=fullName> を呼び出す前に URI を調べて `:` 文字を探し、以前の動作が望ましければそれを削除し、正しい形式として処理させます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=nameWithType>
