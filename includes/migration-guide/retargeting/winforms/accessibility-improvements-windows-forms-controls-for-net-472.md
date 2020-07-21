---
ms.openlocfilehash: cc3c2c2be179842f87be8892d057a6c4138086cb
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614877"
---
### <a name="accessibility-improvements-in-windows-forms-controls-for-net-472"></a>.NET 4.7.2 の Windows フォーム コントロールでのアクセシビリティの向上

#### <a name="details"></a>説明

Windows フォーム フレームワークは、アクセシビリティ テクノロジでの動作の向上により、Windows フォームのお客様のサポートが向上しています。 次のような点が変更されます。

- ハイ コントラスト モード中の表示が向上する変更。
- DataGridView コントロールと MenuStrip コントロールでのキーボード ナビゲーションが向上する変更。
- ナレーターとのやり取りの変更。

#### <a name="suggestion"></a>提案される解決策

**これらの変更を選択する方法と選択しない方法** アプリケーションでこれらの変更を利用するには、.NET Framework 4.7.2 以降で実行する必要があります。 アプリケーションは、次のいずれかの方法でこれらの変更を利用できます。

- .NET Framework 4.7.2 を対象にして再コンパイルします。 .NET Framework 4.7.2 以降を対象とする Windows フォーム アプリケーションでは、これらのアクセシビリティの変更が既定で有効になります。
- .NET Framework 4.7.1 以前を対象にして、下の例のように、app.config ファイルの `<runtime>` セクションに次の [AppContext スイッチ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)を追加し、それを `false` に設定することで、以前のアクセシビリティ動作を無効にします。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7"/>
  </startup>
  <runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true/false;key2=true/false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
  </runtime>
</configuration>
```

.NET Framework 4.7.2 で追加されたアクセシビリティ機能にオプトインするには、.NET Framework 4.7.1 のアクセシビリティ機能にもオプトインする必要があることに注意してください。 .NET Framework 4.7.2 以降を対象とするアプリケーションで以前のアクセシビリティ動作を残す場合、この AppContext スイッチを明示的に `true` に設定することで以前のアクセシビリティ機能を選択できます。

**ハイ コントラスト テーマでの OS で定義された色の使用**

- <xref:System.Windows.Forms.ToolStripDropDownButton> のドロップダウン矢印が、OS で定義されているハイ コントラスト テーマの色を使うようになりました。
- <xref:System.Windows.Forms.ButtonBase.FlatStyle> が <xref:System.Windows.Forms.FlatStyle.Flat?displayProperty=nameWithType> または <xref:System.Windows.Forms.FlatStyle.Popup?displayProperty=nameWithType> に設定された <xref:System.Windows.Forms.Button>、<xref:System.Windows.Forms.RadioButton>、<xref:System.Windows.Forms.CheckBox> コントロールは、ハイ コントラスト テーマが選択されているときは OS で定義された色を使用するようになります。 以前は、テキストと背景の色はコントラストが同じで、見分けるのが困難でした。
- <xref:System.Windows.Forms.Control.Enabled> プロパティが `false` に設定された <xref:System.Windows.Forms.GroupBox> に含まれるコントロールは、OS で定義されているハイ コントラスト テーマの色を使うようになります。
- <xref:System.Windows.Forms.ToolStripButton>、<xref:System.Windows.Forms.ToolStripComboBox>、<xref:System.Windows.Forms.ToolStripDropDownButton> コントロールは、ハイ コントラスト モードでの明度コントラストの比率が高くなりました。
- <xref:System.Windows.Forms.DataGridViewLinkCell> は <xref:System.Windows.Forms.DataGridViewLinkCell.LinkColor?displayProperty=nameWithType> プロパティに対し OS で定義されているハイ コントラスト テーマの色を既定で使うようになります。
注:Windows 10 では、一部のハイ コントラストのシステム カラーの値が変更されています。 Windows フォームのフレームワークは、Win32 フレームワークに基づいています。 最も快適に利用するためには、最新版の Windows で実行し、テスト アプリケーションに app.manifest ファイルを追加して最新の OS 変更を選択し、次のコードのコメントを解除します。

```xml
<!-- Windows 10 -->
<supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
```

**ナレーター サポートが改善されました**

- ナレーターは、<xref:System.Windows.Forms.ToolStripMenuItem> のテキストを読み上げるときに、<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys?displayProperty=nameWithType> プロパティの値を読み上げるようになります。
- <xref:System.Windows.Forms.ToolStripMenuItem> の <xref:System.Windows.Forms.Control.Enabled> プロパティが `false` に設定されている場合、ナレーターはそれを示すようになります。
- ナレーターは、<xref:System.Windows.Forms.ListView.CheckBoxes?displayProperty=nameWithType> プロパティが `true` に設定されているとき、チェック ボックスの状態に関するフィードバックを提供するようになります。
- ナレーター スキャン モードのフォーカス順序が、ClickOnce ダウンロード ダイアログ ウィンドウでのコントロールの視覚的な順序と一致するようになります。

**DataGridView のアクセシビリティ サポートの向上**

- <xref:System.Windows.Forms.DataGridView> の行をキーボードを使って並べ替えられるようになります。 ユーザーは、F3 キーを使って現在の列で並べ替えることができます。
- <xref:System.Windows.Forms.DataGridView.SelectionMode?displayProperty=nameWithType> が <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType> に設定されていると、ユーザーが現在の行のセルを Tab で移動するとき、列ヘッダーの色が変わって現在の列を示します。
- <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Parent?displayProperty=nameWithType> プロパティは、正しい親コントロールを返します。

**視覚的な手掛かりの向上**

- <xref:System.Windows.Forms.ButtonBase.Text> プロパティが空の <xref:System.Windows.Forms.RadioButton> および <xref:System.Windows.Forms.CheckBox> コントロールは、フォーカスを受け取るとフォーカス インジケーターを表示するようになりました。

**強化されたプロパティ グリッドのサポート**

- <xref:System.Windows.Forms.PropertyGrid> コントロールの子要素は、PropertyGrid 要素が有効になっている場合にのみ、<xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> プロパティに対して `true` を返すようになりました。
- <xref:System.Windows.Forms.PropertyGrid> コントロールの子要素は、PropertyGrid 要素をユーザーが変更できる場合にのみ、<xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> プロパティに対して `false` を返すようになりました。
UI オートメーションの概要については、「[UI オートメーションの概要](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-overview)」を参照してください。</p>**キーボード ナビゲーションの向上**

- <xref:System.Windows.Forms.ToolStripButton> は、<xref:System.Windows.Forms.ToolStripPanel.TabStop> プロパティが `true` に設定された <xref:System.Windows.Forms.ToolStripPanel> 内に含まれているときに、フォーカスできるようになりました。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
