---
ms.openlocfilehash: 11c04441dcec260f0bfb90f6ed2b919b1545b382
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721646"
---
### <a name="modernization-of-the-folderbrowserdialog"></a>FolderBrowserDialog の最新化

<xref:System.Windows.Forms.FolderBrowserDialog> コントロールが、.NET Core の Windows フォーム アプリケーションで変更されています。

#### <a name="change-description"></a>変更の説明

.NET Framework で Windows フォームは <xref:System.Windows.Forms.FolderBrowserDialog> コントロールに対し、次のダイアログを使用します。

![.NET Framework の FolderBrowserDialogControl](~/docs/images/core-changes/windowsforms/modernized-folderbrowserdialog/folderdlg-framework.png)

.NET Core 3.0 では、Windows フォームは、Windows Vista で導入された次の新しい COM ベースのコントロールを使用します。

![.NET Core の FolderBrowserDialogControl](~/docs/images/core-changes/windowsforms/modernized-folderbrowserdialog/folderdlg-core.png)

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨アクション

このダイアログは、自動的にアップグレードされます。

元のダイアログを保持したい場合、ダイアログを表示する前に、次のコード断片で示されるとおり、<xref:System.Windows.Forms.FolderBrowserDialog.AutoUpgradeEnabled?displayProperty=nameWithType> プロパティを `false` に設定します。

```csharp
var dialog = new FolderBrowserDialog();
dialog.AutoUpgradeEnabled = false;
dialog.ShowDialog();
```

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.FolderBrowserDialog>

<!--

#### Affected APIs

- `T:System.Windows.Forms.FolderBrowserDialog`

-->
