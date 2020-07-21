---
ms.openlocfilehash: 3f330d5e601d599231ef0336b785e677fe1d114e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616079"
---
### <a name="dataobjectgetdata-now-retrieves-data-as-utf-8"></a>DataObject.GetData は、データを UTF-8 として取得するようになりました

#### <a name="details"></a>説明

.NET Framework 4 を対象とするアプリまたは .NET Framework 4.5.1 以前のバージョンで実行されるアプリでは、`DataObject.GetData` は HTML 形式のデータを ASCII 文字列として取得します。 結果として、非 ASCII 文字 (ASCII コードが 0x7F よりも大きい文字) は 2 つのランダムな文字で表されます。<p/>.NET Framework 4.5 以降を対象とするアプリ、および.NET Framework 4.5.2 で実行するアプリでは、`DataObject.GetData` は HTML 形式のデータを UTF-8 として取得し、これは、0x7F よりも大きい文字を正しく表します。

#### <a name="suggestion"></a>提案される解決策

HTML 形式の文字列を使用するエンコーディングの問題に対する回避策 (例: クリップボードから取得した HTML 文字列を <xref:System.Text.UTF8Encoding.GetString(System.Byte[],System.Int32,System.Int32)?displayProperty=fullName> に渡して明示的にエンコードすること) を実装し、アプリをバージョン 4 から 4.5 へ再ターゲットしている場合は、その回避策を削除する必要があります。何らかの理由で古い動作を必要とする場合は、アプリのターゲットを .NET Framework 4.0 にしてその動作を得ることができます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.5.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.DataObject.GetData(System.String)?displayProperty=nameWithType>
- <xref:System.Windows.DataObject.GetData(System.Type)?displayProperty=nameWithType>
- <xref:System.Windows.DataObject.GetData(System.String,System.Boolean)?displayProperty=nameWithType>
