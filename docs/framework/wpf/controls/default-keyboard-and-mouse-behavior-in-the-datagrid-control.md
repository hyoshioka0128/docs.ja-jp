---
title: DataGrid コントロールの既定のキーボード動作とマウス動作
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid [WPF], keyboard behavior
- DataGrid [WPF], mouse behavior
- keyboard behavior [WPF], DataGrid
- mouse behavior [WPF], DataGrid
ms.assetid: 563b8854-ca39-4d97-8235-17eaa0f93c8d
ms.openlocfilehash: a518c6123b21ae62742071a0b26c6a09fa272b17
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591274"
---
# <a name="default-keyboard-and-mouse-behavior-in-the-datagrid-control"></a>DataGrid コントロールの既定のキーボード動作とマウス動作
このトピックでは、ユーザーがキーボードとマウスを使用して、<xref:System.Windows.Controls.DataGrid> コントロールとどのようにやりとりできるかどうかについて説明します。  
  
 <xref:System.Windows.Controls.DataGrid> との一般的なやり取りには、ナビゲーション、選択、編集などがあります。 選択の動作は、<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> および <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A> プロパティに影響を受けます。 このトピックで説明されている動作を発生させる既定値は、<xref:System.Windows.Controls.DataGridSelectionMode.Extended?displayProperty=nameWithType> と <xref:System.Windows.Controls.DataGridSelectionUnit.FullRow?displayProperty=nameWithType> です。 これらの値を変更すると、説明されているものとは異なる動作が発生する可能性があります。 セルが編集モードの場合、編集コントロールによって、<xref:System.Windows.Controls.DataGrid> の標準的なキーボード動作がオーバーライドされることがあります。  
  
## <a name="default-keyboard-behavior"></a>既定のキーボード動作  
 次の表には、<xref:System.Windows.Controls.DataGrid> の既定のキーボード動作が一覧表示されています。  
  
|キーまたはキーの組み合わせ|説明|  
|----------------------------|-----------------|  
|↓|現在のセルのすぐ下のセルにフォーカスを移動します。 フォーカスが最後の行にある場合は、↓ キーを押しても何も行われません。|  
|↑|現在のセルのすぐ上のセルにフォーカスを移動します。 フォーカスが最初の行にある場合は、↑ キーを押しても何も行われません。|  
|←|行の前のセルにフォーカスを移動します。 フォーカスが行の最初のセルにある場合は、← キーを押しても何も行われません。|  
|→|行の次のセルにフォーカスを移動します。 フォーカスが行の最後のセルにある場合は、→ キーを押しても何も行われません。|  
|ホーム|現在の行の最初のセルにフォーカスを移動します。|  
|End|現在の行の最後のセルにフォーカスを移動します。|  
|PageDown|行がグループ化されていない場合は、完全に表示されている行の数だけ下にコントロールをスクロールします。 列を変更せずに、完全に表示されている最後の行にフォーカスを移動します。<br /><br /> 行がグループ化されている場合は、列を変更せずに、<xref:System.Windows.Controls.DataGrid> の最後の行にフォーカスを移動します。|  
|PageUp|行がグループ化されていない場合は、完全に表示されている行の数だけ上にコントロールをスクロールします。 列を変更せずに、表示されている最初の行にフォーカスを移動します。<br /><br /> 行がグループ化されている場合は、列を変更せずに、<xref:System.Windows.Controls.DataGrid> の最初の行にフォーカスを移動します。|  
|Tab|現在の行の次のセルにフォーカスを移動します。 フォーカスが行の最後のセルにある場合は、次の行の最初のセルにフォーカスを移動します。 フォーカスがコントロールの最後のセルにある場合は、親コンテナーのタブ オーダーで次のコントロールにフォーカスを移動します。<br /><br /> 現在のセルが編集モードであり、Tab キーを押すとフォーカスが現在の行から移動する場合、行に加えられた変更はすべて、フォーカスが変更される前にコミットされます。|  
|Shift + Tab|現在の行の前のセルにフォーカスを移動します。 フォーカスが既に行の最初のセルにある場合は、前の行の最後のセルにフォーカスを移動します。 フォーカスがコントロールの最初のセルにある場合は、親コンテナーのタブ オーダーで前のコントロールにフォーカスを移動します。<br /><br /> 現在のセルが編集モードであり、Tab キーを押すとフォーカスが現在の行から移動する場合、行に加えられた変更はすべて、フォーカスが変更される前にコミットされます。|  
|Ctrl +↓|現在の列の最後のセルにフォーカスを移動します。|  
|Ctrl + ↑|現在の列の最初のセルにフォーカスを移動します。|  
|Ctrl + →|現在の行の最後のセルにフォーカスを移動します。|  
|Ctrl + ←|現在の行の最初のセルにフォーカスを移動します。|  
|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;Home|コントロールの最初のセルにフォーカスを移動します。|  
|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;End|コントロールの最後のセルにフォーカスを移動します。|  
|Ctrl + PageDown|PageDown と同じです。|  
|Ctrl + PageUp|PageUP と同じです。|  
|F2|<xref:System.Windows.Controls.DataGrid.IsReadOnly%2A?displayProperty=nameWithType> プロパティが `false` で、<xref:System.Windows.Controls.DataGridColumn.IsReadOnly%2A?displayProperty=nameWithType> プロパティが現在の列に対して `false` である場合は、現在のセルをセルの編集モードにします。|  
|Enter|現在のセルと行に対するすべての変更をコミットし、現在のセルのすぐ下にあるセルにフォーカスを移動します。 フォーカスが最後の行にある場合は、フォーカスを移動せずにすべての変更をコミットします。|  
|ESC|コントロールが編集モードの場合は、編集をキャンセルし、コントロールで加えられたすべての変更を元に戻します。 基になるデータ ソースで <xref:System.ComponentModel.IEditableObject> を実装している場合は、ESC キーを 2 回押すと、行全体の編集モードがキャンセルされます。|  
|BackSpace|セルを編集するときに、カーソルの前の文字を削除します。|  
|Del|セルを編集するときに、カーソルの後の文字を削除します。|  
|Ctrl + Enter|フォーカスを移動せずに、現在のセルに対するすべての変更をコミットします。|  
|Ctrl + A|<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> が <xref:System.Windows.Controls.DataGridSelectionMode.Extended> に設定されている場合は、<xref:System.Windows.Controls.DataGrid> 内のすべての行を選択します。|  
  
## <a name="selection-keys"></a>選択キー  
 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> プロパティが <xref:System.Windows.Controls.DataGridSelectionMode.Extended> に設定されている場合、ナビゲーションの動作は変わりませんが、Shift キーを押しながらキーボードで移動する (Ctrl + Shift を含む) と、複数行の選択が変更されます。 ナビゲーションが開始される前に、コントロールでは現在の行がアンカー行としてマークされます。 Shift キーを押しながら移動すると、選択範囲に、アンカー行と現在の行の間のすべての行が含まれます。  
  
 次の選択キーでは、複数行の選択を変更します。  
  
- Shift + ↓  
  
- Shift + ↑  
  
- Shift + PageDown  
  
- Shift + PageUp  
  
- Ctrl + Shift + ↓  
  
- Ctrl + Shift + ↑  
  
- Ctrl</localizedText> + <localizedText>Shift</localizedText> + <localizedText>Home  
  
- Ctrl</localizedText> + <localizedText>Shift</localizedText> + <localizedText>End  
  
## <a name="default-mouse-behavior"></a>既定のマウス動作  
 次の表には、<xref:System.Windows.Controls.DataGrid> の既定のマウス動作が一覧表示されています。  
  
|マウス操作|説明|  
|------------------|-----------------|  
|選択されていない行をクリックする|クリックされた行を現在の行にし、クリックされたセルを現在のセルにします。|  
|現在のセルをクリックする|現在のセルを編集モードにします。|  
|列のヘッダー セルをドラッグする|<xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A?displayProperty=nameWithType> プロパティが `true` で、<xref:System.Windows.Controls.DataGridColumn.CanUserReorder%2A?displayProperty=nameWithType> プロパティが現在の列に対して `true` である場合は、新しい位置にドロップできるように列を移動します。|  
|列のヘッダー区切り線をドラッグする|<xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> プロパティが `true` で、<xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> プロパティが現在の列に対して `true` である場合は、列のサイズを変更します。|  
|列ヘッダーの区切り線をダブルクリックする|<xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> プロパティが `true` で、<xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> プロパティが現在の列に対して `true` である場合は、<xref:System.Windows.Controls.DataGridLength.Auto%2A> サイズ変更モードを使用して、列のサイズを自動的に変更します。|  
|列のヘッダー セルをクリックする|<xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A?displayProperty=nameWithType> プロパティが `true` で、<xref:System.Windows.Controls.DataGridColumn.CanUserSort%2A?displayProperty=nameWithType> プロパティが現在の列に対して `true` である場合は、列を並べ替えます。<br /><br /> 既に並べ替えられている列のヘッダーをクリックすると、その列の並べ替え方向が逆になります。<br /><br /> 複数の列ヘッダーをクリックしながら Shift キーを押すと、クリックした順に複数の列で並べ替えられます。|  
|Ctrl キーを押しながら行をクリックする|<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> が <xref:System.Windows.Controls.DataGridSelectionMode.Extended> に設定されている場合は、連続していない複数行の選択を変更します。<br /><br /> 行が既に選択されている場合は、行の選択を解除します。|  
|Shift キーを押しながら行をクリックする|<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> が <xref:System.Windows.Controls.DataGridSelectionMode.Extended> に設定されている場合は、連続する複数行の選択を変更します。|  
|行のグループ ヘッダーをクリックする|グループを展開または折りたたみます。|  
|<xref:System.Windows.Controls.DataGrid> の左上隅にある [すべて選択] ボタンをクリックする|<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> が <xref:System.Windows.Controls.DataGridSelectionMode.Extended> に設定されている場合は、<xref:System.Windows.Controls.DataGrid> 内のすべての行を選択します。|  
  
## <a name="mouse-selection"></a>マウスの選択  
 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> プロパティが <xref:System.Windows.Controls.DataGridSelectionMode.Extended> に設定されている場合、Ctrl または Shift キーを押しながら行をクリックすると、複数行の選択が変更されます。  
  
 Ctrl キーを押しながら行をクリックすると、その行の選択状態が変わりますが、他のすべての行の現在の選択状態は保持されます。 隣接していない行を選択する場合は、このようにします。  
  
 Shift キーを押しながら行をクリックすると、現在の行と、クリックする前に現在の行の位置にあったアンカー行の間のすべての行が選択範囲に含まれます。 Shift キーを押しながら続けてクリックすると、現在の行は変わりますが、アンカー行は変わりません。 隣接する行の範囲を選択する場合は、このようにします。  
  
 Ctrl + Shift を組み合わせると、隣接する行の隣接していない範囲を選択できます。 これを行うには、前述のように、Shift キーを押しながらクリックして最初の範囲を選択します。 行の最初の範囲が選択された後、Ctrl キーを押しながらクリックして次の範囲の最初の行を選択し、Ctrl キーを押しながら Shift キーを押して次の範囲の最後の行をクリックします。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DataGrid>
- <xref:System.Windows.Controls.DataGrid.SelectionMode%2A>
