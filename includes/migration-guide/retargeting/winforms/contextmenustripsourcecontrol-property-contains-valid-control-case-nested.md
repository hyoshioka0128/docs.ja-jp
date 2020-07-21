---
ms.openlocfilehash: 97299ddb9bee89c792ddb3d2b9c37516180996f7
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614878"
---
### <a name="contextmenustripsourcecontrol-property-contains-a-valid-control-in-the-case-of-nested-toolstripmenuitems"></a>入れ子になった ToolStripMenuItems の場合、ContextMenuStrip.SourceControl プロパティには有効なコントロールが含まれる

#### <a name="details"></a>説明

.NET Framework 4.7.1 およびそれより前のバージョンの <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> プロパティは、ユーザーが入れ子になった <xref:System.Windows.Forms.ToolStripMenuItem> コントロールからメニューを開いたとき、正しくない null を返します。 .NET Framework 4.7.2 およびそれ以降では、<xref:System.Windows.Forms.ContextMenuStrip.SourceControl> プロパティには常に実際のソース コントロールが設定されます。

#### <a name="suggestion"></a>提案される解決策

**これらの変更を選択する方法と選択しない方法** アプリケーションでこれらの変更を利用するには、.NET Framework 4.7.2 以降で実行する必要があります。 アプリケーションは、次のいずれかの方法でこれらの変更を利用できます。

- .NET Framework 4.7.2 を対象にします。 .NET Framework 4.7.2 以降を対象とする Windows フォーム アプリケーションでは、この変更が既定で有効になります。
- .NET Framework 4.7.1 以前を対象にして、下の例のように、app.config ファイルの `<runtime>` セクションに次の [AppContext スイッチ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)を追加し、それを `false` に設定することで、以前のアクセシビリティ動作を無効にします。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue=false"/>
</runtime>
```

.NET Framework 4.7.2 以降を対象とするアプリケーションで以前の動作を残す場合、この AppContext スイッチを明示的に `true` に設定することで、以前のソース コントロール値を選択できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType>
