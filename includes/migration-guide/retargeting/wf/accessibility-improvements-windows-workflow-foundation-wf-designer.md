---
ms.openlocfilehash: d420be76645fc71ac922542fa49f799a473e9a83
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614850"
---
### <a name="accessibility-improvements-in-windows-workflow-foundation-wf-workflow-designer"></a>Windows Workflow Foundation (WF) ワークフロー デザイナーでのアクセシビリティの向上

#### <a name="details"></a>説明

Windows Workflow Foundation (WF) ワークフロー デザイナーは、アクセシビリティ テクノロジによって操作性が向上しています。 次のような改善点があります。

- 一部のコントロールで、タブ オーダーが左から右、上から下に変更されます:
- <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの関連付けデータを設定するための関連付けの初期化ウィンドウ
- <xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.SendReply>、および <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティのコンテンツ定義ウィンドウ
- キーボードで利用できる機能が増えます:
- アクティビティのプロパティを編集する際、プロパティ グループに初めてフォーカスを設定したときに、プロパティ グループをキーボードで折りたたむことができます。
- 警告アイコンにキーボードでアクセスできるようになりました。
- [プロパティ] ウィンドウの [その他のプロパティ] ボタンに、キーボードでアクセスできるようになりました。
- キーボードを使って、ワークフロー デザイナーの [引数] および [変数] ウィンドウのヘッダー項目にアクセスできるようになりました。
- 次のような場合に、フォーカスのある項目の可視性が向上しました:
- ワークフロー デザイナーおよびアクティビティ デザイナーで使われているデータ グリッドへの行の追加。
- <xref:System.ServiceModel.Activities.ReceiveReply> および <xref:System.ServiceModel.Activities.SendReply> アクティビティ内のフィールド間の Tab 移動。
- 変数または引数の既定値の設定
- スクリーン リーダーが正しく認識できるようになりました:
- ワークフロー デザイナーで設定されたブレークポイント。
- <xref:System.Activities.Statements.FlowSwitch%601>、<xref:System.Activities.Statements.FlowDecision>、<xref:System.ServiceModel.Activities.CorrelationScope> アクティビティ。
- <xref:System.ServiceModel.Activities.Receive> アクティビティの内容。
- <xref:System.Activities.Statements.InvokeMethod> アクティビティのターゲットの種類。
- <xref:System.Activities.Statements.TryCatch> アクティビティの [例外] コンボ ボックスと [Finally] セクション。
- メッセージング アクティビティの [メッセージの種類] コンボ ボックス、[関連付け初期化子の追加] ウィンドウのスプリッター、[コンテンツ定義] ウィンドウで、および [CorrelatesOn の定義] ウィンドウ (<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.SendReply>、および <xref:System.ServiceModel.Activities.ReceiveReply>)。
- ステート マシンの遷移と遷移先。
- <xref:System.Activities.Statements.FlowDecision> アクティビティの注釈とコネクタ。
- アクティビティのコンテキスト (右クリック) メニュー。
- プロパティ グリッドの、プロパティ値エディター、[検索のクリア] ボタン、[カテゴリ別] および [アルファベット順] の並べ替えボタン、[式エディター] ダイアログ。
- ワークフロー デザイナーのズーム パーセンテージ。
- <xref:System.Activities.Statements.Parallel> および <xref:System.Activities.Statements.Pick> アクティビティの区切り記号。
- <xref:System.Activities.Statements.InvokeDelegate> アクティビティ。
- ディクショナリ アクティビティの [型の選択] ウィンドウ (`Microsoft.Activities.AddToDictionary&lt;TKey,TValue>`、`Microsoft.Activities.RemoveFromDictionary&lt;TKey,TValue>` など)。
- [.NET 型の参照と選択] ウィンドウ。
- ワークフロー デザイナーでの階層リンク。
- ハイ コントラスト テーマを選ぶと、要素間のコントラスト比の向上や、フォーカス要素に使われる選択ボックスの認識性の向上など、ワークフロー デザイナーとそのコントロールの表示について多くの点が向上していることがわかります。

#### <a name="suggestion"></a>提案される解決策

ワークフロー デザイナーが再ホストされたアプリケーションでは、次のいずれかを行うことでこれらの変更を利用できます。

- .NET Framework 4.7.1 を対象にしてアプリケーションを再コンパイルします。 これらのアクセシビリティの変更が既定で有効になります。
- アプリケーションの対象が .NET Framework 4.7 以前であっても、.NET Framework 4.7.1 上で実行している場合は、次の [AppContext スイッチ](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)を app.config ファイルの `<runtime>` セクションに追加して `false` に設定することにより、従来のアクセシビリティ動作を無効にできます (次の例をご覧ください)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7"/>
  </startup>
  <runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true/false;key2=true/false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
  </runtime>
</configuration>
```

.NET Framework 4.7.1 以降を対象とするアプリケーションで以前のアクセシビリティ動作を残す場合、この AppContext スイッチを明示的に `true` に設定することで以前のアクセシビリティ機能を選択できます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |
