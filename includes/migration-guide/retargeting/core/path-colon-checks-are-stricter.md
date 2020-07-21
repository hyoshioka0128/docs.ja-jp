---
ms.openlocfilehash: 3e4a5936bbac4e77efc5f7e68b55ddf49bae5d43
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614720"
---
### <a name="path-colon-checks-are-stricter"></a>パスのコロン確認が厳密化

#### <a name="details"></a>説明

.NET Framework 4.6.2 では、以前はサポートされていなかったパスをサポートするために (長さと形式の両方で) 数多くの変更が加えられました。 適切なドライブ区切り (コロン) 構文の確認がより正確に行われました。その結果、それ以前は許容されていた、ごく少数のパス API の一部の URI パスがブロックされました。

#### <a name="suggestion"></a>提案される解決策

影響を受ける API に URI を渡す場合、まず、文字列を正規のパスに変更します。<ul><li>URL から手動でスキームを削除します (たとえば、URL から `file://` を削除します)。

- <xref:System.Uri> クラスに URI を渡し、<xref:System.Uri.LocalPath> を使用します。

あるいは、`Switch.System.IO.UseLegacyPathHandling` AppContext スイッチを true に設定し、新しいパス正規化を無効にできます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IO.Path.GetDirectoryName(System.String)?displayProperty=nameWithType>
- <xref:System.IO.Path.GetPathRoot(System.String)?displayProperty=nameWithType>
