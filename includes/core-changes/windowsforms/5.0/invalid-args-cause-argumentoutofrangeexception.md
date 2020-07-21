---
ms.openlocfilehash: f42da00487735acdcc60f876c75e1dfd17103008
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84702445"
---
### <a name="winforms-properties-now-throw-argumentoutofrangeexception"></a>WinForms プロパティによる ArgumentOutOfRangeException のスロー

一部の Windows フォーム プロパティで、無効な引数に対して <xref:System.ArgumentOutOfRangeException> がスローされるようになりました。以前はスローされませんでした。

#### <a name="change-description"></a>変更の説明

以前は、これらのプロパティでは、範囲外の引数が渡されたときに <xref:System.NullReferenceException>、<xref:System.IndexOutOfRangeException>、<xref:System.ArgumentException> などのさまざまな例外がスローされていました。 .NET 5.0 以降、これらのプロパティでは、範囲外の引数が渡されたときに <xref:System.ArgumentOutOfRangeException> がスローされるようになりました。

<xref:System.ArgumentOutOfRangeException> をスローすることは、.NET ランタイムの動作に準拠しています。 また、どの引数が無効であるのかが明確に伝えられることで、デバッグ エクスペリエンスも向上します。

#### <a name="version-introduced"></a>導入されたバージョン

.NET 5.0

#### <a name="recommended-action"></a>推奨アクション

- 無効な引数を渡さないようにコードを更新します。
- 必要に応じて、プロパティを設定するときに <xref:System.ArgumentOutOfRangeException> を処理します。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

次の表に、影響を受けるプロパティとパラメーターの一覧を示します。

> [!div class="mx-tdBreakAll"]
> | プロパティ | パラメーター名 | 追加されたバージョン |
> |-|-|-|
> | <xref:System.Windows.Forms.ListBox.IntegerCollection.Item(System.Int32)?displayProperty=nameWithType> | `index` | 5.0 Preview 5 |
> | <xref:System.Windows.Forms.TreeNode.ImageIndex?displayProperty=nameWithType> | `value` | 5.0 Preview 6 |
> | <xref:System.Windows.Forms.TreeNode.SelectedImageIndex?displayProperty=nameWithType> | `value` | 5.0 Preview 6 |

<!-- 

#### Affected APIs

- `P:System.Windows.Forms.ListBox.IntegerCollection.Item(System.Int32)`
- `P:System.Windows.Forms.TreeNode.ImageIndex`
- `P:System.Windows.Forms.TreeNode.SelectedImageIndex`

-->
