---
ms.openlocfilehash: 0b2d3c1383246d4259c6d906ecf9dab927f4bdb1
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721093"
---
### <a name="default-control-font-changed-to-segoe-ui-9-pt"></a>既定のコントロール フォントが Segoe UI 9 pt に変更されました

#### <a name="change-description"></a>変更の説明

.NET Framework では、<xref:System.Windows.Forms.Control.DefaultFont?displayProperty=nameWithType> プロパティは、`Microsoft Sans Serif 8 pt` に設定されていました。 次の画像は、既定のフォントを使用するウィンドウを示しています。

![.NET Framework の既定のコントロール フォント](~/docs/images/core-changes/windowsforms/control-defaultfont-changed/defaultfont-framework.png)

.NET Core 3.0 以降では、既定のフォントは `Segoe UI 9 pt` (<xref:System.Drawing.SystemFonts.MessageBoxFont?displayProperty=nameWithType> と同じフォント) に設定されています。 この変更により、大きくなった新しい既定のフォント サイズに対応するために、フォームとコントロールのサイズが約 27% 大きくなっています。 次に例を示します。

![.NET Core の既定のコントロール フォント](~/docs/images/core-changes/windowsforms/control-defaultfont-changed/defaultfont-core.png)

この変更は、[Windows ユーザー エクスペリエンス (UX) のガイドライン](/windows/win32/uxguide/vis-fonts#fonts-and-colors)に合わせて行われました。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨アクション

フォームとコントロールのサイズが変更されているため、レンダリングがご使用のアプリケーションで正しく行われることを確認してください。

元のフォントを維持するには、フォームの既定のフォントを `Microsoft Sans Serif 8 pt` に設定します。 次に例を示します。

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

[なし] :

<!--

#### Affected APIs

- Not detectable via API analysis

-->
