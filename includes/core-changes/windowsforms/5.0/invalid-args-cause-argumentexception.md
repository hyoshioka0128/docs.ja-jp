---
ms.openlocfilehash: aab7d8538c875e35c832acc2a6c64beb84d4fb47
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84702444"
---
### <a name="winforms-methods-now-throw-argumentexception"></a>WinForms メソッドで ArgumentException がスローされるようになった

一部の Windows フォーム メソッドで、無効な引数に対して <xref:System.ArgumentException> がスローされるようになりました。以前はスローされませんでした。

#### <a name="change-description"></a>変更の説明

以前は、予期しない型または不適切な型の引数を特定の Windows フォーム メソッドに渡すと、不確定な状態になりました。 .NET 5.0 以降では、そのようなメソッドに無効な引数を渡すと、<xref:System.ArgumentException> がスローされるようになりました。

<xref:System.ArgumentException> をスローすることは、.NET ランタイムの動作に準拠しています。 また、どの引数が無効であるのかが明確に伝えられることで、デバッグ エクスペリエンスも向上します。

次の表では、影響を受けるメソッドとパラメーターを示します。

| メソッド | パラメーター名 | 条件 | 追加されたバージョン |
|-|-|-|-|
| <xref:System.Windows.Forms.TabControl.GetToolTipText(System.Object)?displayProperty=fullName> | `item` | 引数が <xref:System.Windows.Forms.TabPage> 型ではありません。 | 5.0 Preview 1 |
| <xref:System.Windows.Forms.DataFormats.GetFormat(System.String)?displayProperty=fullName> | `format` | 引数が `null`、<xref:System.String.Empty?displayProperty=nameWithType>、または空白です。 | 5.0 Preview 5 |

#### <a name="version-introduced"></a>導入されたバージョン

.NET 5.0

#### <a name="recommended-action"></a>推奨アクション

- 無効な引数を渡さないようにコードを更新します。
- 必要に応じて、メソッドを呼び出したときの <xref:System.ArgumentException> を処理します。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.TabControl.GetToolTipText(System.Object)?displayProperty=fullName>
- <xref:System.Windows.Forms.DataFormats.GetFormat(System.String)?displayProperty=fullName>

<!-- 

#### Affected APIs

- `M:System.Windows.Forms.TabControl.GetToolTipText(System.Object)`
- `M:System.Windows.Forms.DataFormats.GetFormat(System.String)`

-->
