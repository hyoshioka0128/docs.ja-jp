---
title: Windows フォームのアクセシビリティの向上
description: .NET Core Windows フォームが .NET Framework の Windows フォームと比較して、アクセシビリティを向上させる方法について説明します。
ms.date: 04/20/2020
helpviewer_keywords:
- Windows Forms accessibility
- accessibility
author: M-Lipin
ms.openlocfilehash: 30eb8b3bd0aaf646ea23f4f036e822f9bba78dc4
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739764"
---
# <a name="accessibility-improvements-in-windows-forms-controls-for-net-core-30"></a>NET Core 3.0 の Windows フォーム コントロールのアクセシビリティの向上

Windows フォームでは、ユーザー補助テクノロジの使用方法を改善し、Windows フォームの顧客をサポートしています。 次のような改善点があります。

- ナレーターを含む、ユーザー補助クライアント アプリケーションとの対話のさまざまな領域の変更。
- アクセス可能な階層の変更 (UI オートメーション ツリー間の移動の改善)。
- キーボード ナビゲーションの変更点。

> [!IMPORTANT]
> NET Framework 4.7.1 から .NET Framework 4.8 で行われたアクセシビリティの変更は、.NET Core 3.0 以降に含まれており、既定で有効になっています。 .NET Framework では、アプリケーションが新しいユーザー補助動作を無効にできる互換性スイッチがサポートされています。 一方、.NET Core はこれらの設定をサポートせず、アプリケーションがユーザー補助動作を無効にすることを許可しません。
  
NET Core 3.0 以降、Windows フォーム アプリケーションは、追加の構成を行わずに、すべての新しいアクセシビリティ機能 (.NET Framework 4.7.1 ~ 4.8 で導入) を活用しています。

## <a name="listbox-accessibility-support"></a>リスト ボックス のアクセシビリティ のサポート

コントロールには、次の変更<xref:System.Windows.Forms.ListBox>が適用されます。

- コントロールの UI`ListBox`オートメーション サポートを有効にしました。
- 項目`ListBox`<xref:System.Windows.Automation.ScrollItemPattern>に`ListBox`を追加し、アクセシビリティ イベントの発生と処理、および項目を介したナレーター のナビゲーションを強化することで、アクセシビリティのサポートが向上しました (CapsLock のナビゲーションが正しくなく、コントロールの外部にナビゲーションが意図せずスローされません)。

## <a name="checkedlistbox-accessibility-support"></a>チェックリストボックスアクセシビリティサポート

コントロールには、次の変更<xref:System.Windows.Forms.CheckedListBox>が適用されます。

- エントリの`CheckedListBox`ユーザー補助プロパティによって提供される制限を修正しました。
- 全体的な`ListBox`改善`CheckedListBox`とアクセシビリティ: プロパティ値とイベント モデルを修正しました。

## <a name="combobox-accessibility-support"></a>コンボ ボックス のアクセシビリティ サポート

コントロールには、次の変更<xref:System.Windows.Forms.ComboBox>が適用されます。

- 項目のアクセシビリティ オブジェクト`ComboBox`を取得するプロセスを更新し、項目からハッシュ コードを取得する代わりにアイテムの ID を<xref:System.Object.GetHashCode%2A>生成できるようにしました。

## <a name="datagridview-accessibility-support"></a>アクセシビリティサポート

コントロールには、次の変更<xref:System.Windows.Forms.DataGridView>が適用されます。

- 列、`DataGridView.Bounds`行、セル、および対応するヘッダーのアクセシビリティ プロパティによって提供される修正により、外接する四角形の計算のパフォーマンスが向上しました。 すべてのアクセシビリティの境界は、コントロール全体の境界とビューポートを考慮して、正しく表現されます。
- アクセス可能`Value.IsReadOnly`なクライアント アプリケーションの提供を修正したプロパティ値。 プロパティにセルの状態`IsReadOnly`が正しく表示されるようになりました。
- 最初のセル変更<xref:System.Windows.Forms.DataGridView.CellParsing>のイベント発生に関する問題を修正しました。 セル値は、最初`DataGridView`のコントロールの相互作用を含め、問題なく変更できます。
- Windows`DataGridView`ハイ コントラスト テーマを使用する場合の背景色のコントラストが改善されました。 HC#1、HC#2、およびHCブラックのテーマを使用する場合のデフォルトの背景色を変更`DataGridView`しました。

## <a name="propertygrid-accessibility-support"></a>プロパティ グリッド アクセシビリティ のサポート

コントロールには、次の変更<xref:System.Windows.Forms.PropertyGrid>が適用されます。

- グリッド`PropertyGrid.Bounds`エントリのアクセシビリティ プロパティによって提供される修正により、外接する四角形の計算のパフォーマンスが向上しました。 ここでは、コントロール全体の境界とビューポートを考慮して、すべてのアクセシビリティ境界が正しく表現されています。
- コントロール型名を含めず、コントロールの型名に対する二重アナウンスを回避するために、サブコントロールのアクセシビリティ対応名と説明を修正しました。

## <a name="toolstrip-accessibility-support"></a>ツールストリップ アクセシビリティサポート

コントロールには、次の変更<xref:System.Windows.Forms.ToolStrip>が適用されます。

- 、 、`ToolStrip``MenuStrip`および`StatusStrip`項目のナビゲーションが改善されました。 修正され`ToolStrip``MenuStrip`、シフトタブナビゲーション,Shiftタブ上矢印が押されたときにメニュー項目をバックループし、下部のメニュー要素に移動します。
- アクセシビリティ`MenuStrip`対応ナビゲーションの改善、サブメニューの修正されたメニューアクセス可能なコントロールの種類を 'MenuItem' ではなく 、型 'Menu' のサブメニューにします。

## <a name="printpreviewcontrol-and-printpreviewdialog-accessibility-support"></a>印刷プレビュー コントロールと印刷プレビューダイアログ アクセシビリティ サポート

印刷コントロールには、次の変更が適用されます。

- メニュー項目を介したアクセシビリティ対応ナビゲーション (ナレーター ナビゲーションを含む) が改善されました。
- ハイ コントラスト テーマのサポートが改善され、コントロール要素のコントラストが向上しました。

## <a name="stringcollectioneditor-accessibility-support"></a>アクセシビリティサポート

Windows フォーム デザイナーでは、アクセシビリティ サポートを強化した文字列コレクション エディターが使用されるようになりました。

## <a name="monthcalendar-accessibility-support-available-in-net-core-31"></a>月間予定表のアクセシビリティサポート (.NET Core 3.1 で利用可能)

コントロールには、次の変更<xref:System.Windows.Forms.MonthCalendar>が適用されます。

- コントロールする UI オートメーション`MonthCalendar`サーバー プロバイダーが追加され、UI オートメーション グリッド パターンとテーブル パターン プロバイダーが追加されました。
- コントロールにコントロールのアクセシビリティ名を`MonthCalendar`定義するラベル`MonthCalendar`コントロールがある場合を除いて、_テーブル_アクセス可能なコントロール型を_カレンダー_アクセス可能なコントロール型に_変更します。_
- 選択した制御日の発表`MonthCalendar`が改善されました。
- スクリーン`MonthCalendar`リーダーおよびその他のユーザー補助ツールのコントロール のサポートが強化されました。 現時点では、ユーザーはコントロール要素を移動し、キーボードのみの入力を使用してこれらの要素と対話できます。 ナレーターでは、CAPS + 矢印キーを使用してコントロール要素をナビゲーションし、CAPS + Enter キーを使用して要素の既定のアクションを呼び出します。
- 子要素間の`MonthCalendar`矢印キーナビゲーションを改善し、フォーカスを四角形にします: ナレーターの青フォーカス四角形。
- 指定された座標で子のアクセス`MonthCalendar`可能な要素を取得`MonthCalendar`できるように、コントロール要素のヒット テスト アクションのアクセシビリティが向上しました。

## <a name="tooltips-accessibility-available-in-net-core-31"></a>ツールヒントのアクセシビリティ (.NET Core 3.1 で利用可能)

- NVDA やナレーターなどのスクリーン リーダー アプリケーションによってツールヒント テキストを発表する機能を追加しました。 スクリーン リーダー アプリケーションは、ツールヒントを表示するように構成された Windows フォーム コントロールのキーボードまたはマウスのツールヒントのテキストを発表できるようになりました。

## <a name="ui-automation-support-for-datagridview-propertygrid-listbox-combobox-toolstrip-and-other-controls"></a>データ グリッド ビュー、プロパティ グリッド、リスト ボックス、コンボ ボックス、ツール ストリップ、およびその他のコントロールの UI オートメーションのサポート

UI オートメーションのサポートは、実行時にコントロールに対して有効にされますが、デザイン時には使用されません。 UI オートメーションの概要については、「[UI オートメーションの概要](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-overview)」を参照してください。

## <a name="see-also"></a>関連項目

- [アクセシビリティのベストプラクティス](../ui-automation/accessibility-best-practices.md)」
