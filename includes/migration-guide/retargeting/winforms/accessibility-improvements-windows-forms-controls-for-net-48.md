---
ms.openlocfilehash: e528a41748d9353c96d443f68e15e7a98ee7f4ae
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616273"
---
### <a name="accessibility-improvements-in-windows-forms-controls-for-net-48"></a>.NET 4.8 の Windows フォーム コントロールでのアクセシビリティの改善

#### <a name="details"></a>説明

Windows フォーム フレームワークでは引き続き、アクセシビリティ テクノロジでの動作が改善されており、Windows フォームのお客様のサポートが向上しています。 次のような点が変更されます。

- ハイ コントラスト モード中の表示が向上する変更。
- ナレーターとのやり取りの変更。
- アクセス可能な階層の変更 (UI オートメーション ツリー間の移動の改善)。

#### <a name="suggestion"></a>提案される解決策

**これらの変更を選択する方法と選択しない方法** アプリケーションでこれらの変更を利用するには、.NET Framework 4.8 で実行する必要があります。 アプリケーションでは、次のいずれかの方法でこれらの変更を選択できます。

- .NET Framework 4.8 をターゲットとして再コンパイルします。 .NET Framework 4.8 をターゲットとする Windows フォーム アプリケーションでは、これらのアクセシビリティの変更が既定で有効になります。
- .NET Framework 4.7.2 以前のバージョンをターゲットとし、下の例のように、アプリ構成ファイルの `<runtime>` セクションに次の [AppContext スイッチ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)を追加し、それを `false` に設定することで、以前のアクセシビリティ動作を選択しないようにします。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7"/>
  </startup>
  <runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true/false;key2=true/false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
  </runtime>
</configuration>
```

.NET Framework 4.8 で追加されたアクセシビリティ機能を選択するには、.NET Framework 4.7.1 と 4.7.2 のアクセシビリティ機能も選択する必要があることに注意してください。 .NET Framework 4.8 をターゲットとするアプリケーションで以前のアクセシビリティ動作を残す場合、この AppContext スイッチを明示的に `true` に設定することで、以前のアクセシビリティ機能の使用を選択できます。キーボード ツールヒントの呼び出しサポートを有効にするには、`Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false` 行を AppContextSwitchOverrides 値に追加する必要があります。

```xml
<AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false" />
```

この機能を有効にするには、.NET Framework 4.7.1 から 4.8 の前述のアクセシビリティ機能を選択する必要があることに注意してください。 また、どのアクセシビリティ機能も選択されていないが、ツールヒントに機能が選択されていることが示される場合は、これらの機能への初回アクセス時に、ランタイムの <xref:System.NotSupportedException> がスローされます。 例外メッセージには、キーボードのツールヒントではレベル 3 のアクセシビリティ機能の強化を有効にする必要があることが示されます。

**ハイ コントラスト テーマでの OS で定義された色の使用**

- ハイ コントラストのテーマが改善されました。

**ナレーター サポートが改善されました**

- ナレーターで、<xref:System.Windows.Forms.DataGridViewCell> のアクセス可能な名前を読み上げるときに、<xref:System.Windows.Forms.DataGridViewColumn> の並べ替えの方向を読み上げるようになりました。

**CheckedListBox アクセシビリティ サポートの改善**

- <xref:System.Windows.Forms.CheckedListBox> コントロールのナレーター サポートが改善されました。 キーボードを使用して <xref:System.Windows.Forms.CheckedListBox> コントロールに移動するときに、ナレーターでは <xref:System.Windows.Forms.CheckedListBox> 項目にフォーカスし、それを読み上げます。
- 空の CheckedListBox コントロールでは、コントロールがフォーカスされたときに、仮想の最初の項目に対してフォーカスを示す四角形が描画されるようになりました。

**ComboBox アクセシビリティ サポートの改善**

- UI オートメーション通知やその他の UI オートメーション機能を使用できる、<xref:System.Windows.Forms.ComboBox> コントロールの UI オートメーション サポートが有効になりました。
**DataGridView のアクセシビリティ サポートの向上**

- UI オートメーション通知やその他の UI オートメーション機能を使用できる、<xref:System.Windows.Forms.DataGridView> コントロールの UI オートメーション サポートが有効になりました。
- <xref:System.Windows.Forms.DataGridViewComboBoxEditingControl> または <xref:System.Windows.Forms.DataGridViewTextBoxEditingControl> に対応する UI オートメーション要素が、対応する編集セルの子になりました。

**LinkLabel アクセシビリティ サポートの改善**

- <xref:System.Windows.Forms.LinkLabel> コントロールのアクセシビリティが改善されました。対応する <xref:System.Windows.Forms.LinkLabel> コントロールが無効になっている場合、ナレーターではリンクの無効状態が読み上げられます。

**ProgressBar アクセシビリティ サポートの改善**

- UI オートメーション通知やその他の UI オートメーション機能を使用できる、<xref:System.Windows.Forms.ProgressBar> コントロールの UI オートメーション サポートが有効になりました。 開発者は、進行状況を示すためにナレーターで読み上げることができる、UI オートメーション通知を使用できるようになりました。
UI オートメーション通知イベントを含む、UI オートメーション イベントの概要については、「[UI オートメーション イベントの概要](https://docs.microsoft.com/windows/desktop/WinAuto/uiauto-eventsoverview)」を参照してください。

**PropertyGrid アクセシビリティ サポートの改善**

- UI オートメーション通知やその他の UI オートメーション機能を使用できる、<xref:System.Windows.Forms.PropertyGrid> コントロールの UI オートメーション サポートが有効になりました。
- 現在編集されているプロパティに対応する UI オートメーション要素が、対応するプロパティ項目の UI オートメーション要素の子になりました。
- 親の <xref:System.Windows.Forms.PropertyGrid> コントロールがカテゴリ ビューに設定されている場合、UI オートメーション プロパティ項目の要素は、対応するカテゴリ要素の子になります。

**ToolStrip サポートの改善**

- UI オートメーション通知やその他の UI オートメーション機能を使用できる、<xref:System.Windows.Forms.ToolStrip> コントロールの UI オートメーション サポートが有効になりました。
- <xref:System.Windows.Forms.ToolStrip> 項目間の移動が改善されました。
- 項目モードでは、ナレーターのフォーカスは非表示にならず、非表示項目には移動しません。

**視覚的な手掛かりの向上**

- 空の <xref:System.Windows.Forms.CheckedListBox> コントロールでは、フォーカスを受け取ったときに、フォーカス インジケーターが表示されるようになりました。
メモ:UI オートメーション サポートは、実行時のコントロールでは有効になりますが、設計時には使用されません。 UI オートメーションの概要については、「[UI オートメーションの概要](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-overview)」を参照してください。

**キーボードでのコントロールのツールヒントの呼び出し**

- キーボードを使用してコントロールにフォーカスすることで、コントロール ツールヒントを呼び出せるようになりました。 この機能は、アプリケーションに対して明示的に有効にする必要があります (「 **&quot;これらの変更を選択する方法と選択しない方法&quot;** 」セクションを参照)

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.8         |
| 種類    | 再ターゲット中 |
