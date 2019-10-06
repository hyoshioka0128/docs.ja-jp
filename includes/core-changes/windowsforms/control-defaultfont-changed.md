---
ms.openlocfilehash: 843007ac6467584fbe6350b6ea19ef67609d73e2
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216913"
---
### <a name="controldefaultfont-changed-to-segoe-ui-9pt"></a>`Control.DefaultFont` の `Segoe UI 9pt` への変更

#### <a name="change-description"></a>変更の説明

.NET Framework では、<xref:System.Windows.Forms.Control.DefaultFont?displayProperty=nameWithType> プロパティは、`Microsoft Sans Serif 8pt` に設定されていました。 次は、既定のフォントを使用するウィンドウの図です。

![.NET Framework の既定のコントロール フォント](~/docs/images/core-changes/windowsforms/control-defaultfont-changed/defaultfont-framework.png)

これは、.NET Core の .NET Core 3.0 以降で `Segoe UI 9pt` に設定されています (<xref:System.Drawing.SystemFonts.MessageBoxFont?displayProperty=nameWithType> と同じフォント)。 この変更により、大きくなった新しい既定のフォント サイズに対応するために、フォームとコントロールのサイズが約 27% 大きくなっています。 次に例を示します。

![.NET Core の既定のコントロールのフォント](~/docs/images/core-changes/windowsforms/control-defaultfont-changed/defaultfont-core.png)

この変更は、[Windows UX のガイドライン](https://docs.microsoft.com/windows/win32/uxguide/vis-fonts#fonts-and-colors)に合わせて行われました。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨される操作

フォームとコントロールのサイズが変更されているため、レンダリングがご使用のアプリケーションで正しく行われることを確認してください。

元のフォントを維持するには、フォームの既定のフォントを `Microsoft Sans Serif 8pt` に設定します。 次に例を示します。

```csharp
public MyForm()
{
    InitializeComponent();
    Font = new Font(new FontFamily("Microsoft Sans Serif"), 8f);
}
```

#### <a name="category"></a>カテゴリ

- Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

なし。

<!--

### Affected APIs

- Not detectable via API analysis

-->
