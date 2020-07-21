---
ms.openlocfilehash: a20fad5f9c95e59c14ffd91f4921cf8bfab443cd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621188"
---
### <a name="unicode-standard-version-80-categories-now-supported"></a>Unicode 標準バージョン 8.0 のカテゴリのサポート開始

#### <a name="details"></a>説明

.NET Framework 4.6.2 で、Unicode データが Unicode 標準バージョン 6.3 からバージョン 8.0 にアップグレードされました。  .NET Framework 4.6.2 で Unicode 文字カテゴリを要求すると、いくつかの結果が以前の .NET Framework バージョンの結果と一致しない可能性があります。  この変更は、主にチェロキーの音節、新タイ ロ文字の母音記号および声調記号に影響します。

#### <a name="suggestion"></a>提案される解決策

コードを確認し、ハードコーディングされた Unicode 文字カテゴリに依存するロジックを削除/変更します。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Char.GetUnicodeCategory(System.Char)?displayProperty=nameWithType></li><li><xref:System.Globalization.CharUnicodeInfo.GetUnicodeCategory(System.Char)?displayProperty=nameWithType></li><li><xref:System.Globalization.CharUnicodeInfo.GetUnicodeCategory(System.String,System.Int32)?displayProperty=nameWithType></li></ul>|
