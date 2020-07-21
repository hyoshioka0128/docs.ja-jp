---
title: '方法: TableLayoutPanel コントロールの列と行を編集する'
description: '[列と行のスタイル] ダイアログボックスを使用して、Windows フォームコントロールの行と列を編集する方法について説明します。'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor
helpviewer_keywords:
- columns [Windows Forms], editing
- TableLayoutPanel control [Windows Forms], editing
- rows [Windows Forms], editing
ms.assetid: c367ed43-40dc-49eb-9e0f-ba70e83dfec0
ms.openlocfilehash: cfd2ca4be5d5a2658a9a129d911f1dba9670ccfd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619352"
---
# <a name="how-to-edit-columns-and-rows-in-a-tablelayoutpanel-control"></a>方法: TableLayoutPanel コントロールの列と行を編集する

[ <xref:System.Windows.Forms.TableLayoutPanel> **列と行のスタイル**] ダイアログボックスと呼ばれるコントロールのコレクションエディターを使用して、コントロールの行と列を編集できます。

> [!NOTE]
> コントロールが複数の行または列にまたがるようにするには、 `RowSpan` コントロールのプロパティとプロパティを設定し `ColumnSpan` ます。 詳細については、「 [Walkthrough: Arranging Controls on Windows Forms Using a TableLayoutPanel](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)」を参照してください。
>
> セル内にコントロールを配置する場合、またはコントロールをセル内に引き伸ばす場合は、コントロールのプロパティを使用し <xref:System.Windows.Forms.Control.Anchor%2A> ます。 詳細については、「 [Walkthrough: Arranging Controls on Windows Forms Using a TableLayoutPanel](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)」を参照してください。

## <a name="to-edit-rows-and-columns"></a>行と列を編集するには

1. <xref:System.Windows.Forms.TableLayoutPanel> ツールボックス **から** コントロールをフォームにドラッグします。

2. <xref:System.Windows.Forms.TableLayoutPanel>コントロールのデザイナーの [アクション] グリフ ( ![ 小さい黒い矢印) をクリック ](./media/designer-actions-glyph.gif) し、[**行と列の編集**] を選択して [**列と行のスタイル**] ダイアログボックスを開きます。 また、コントロールを右クリック <xref:System.Windows.Forms.TableLayoutPanel> し、ショートカットメニューの [**行と列の編集**] をクリックすることもできます。

3. 列を追加または削除するには、[**メンバーの種類**] ボックスの一覧から**列**を選択します。

4. 行を追加または削除するには、[**メンバーの種類**] ボックスの一覧から [**行**] を選択します。

5. **メンバー**リストの末尾に行または列を追加するには、[**追加**] ボタンをクリックします。

6. 一覧で現在選択されている項目の前に行または列を追加するには、[**挿入**] ボタンをクリックします。

7. 行または列を追加する場合は、新しい行または列の**サイズの種類**を選択します。 詳細については、「<xref:System.Windows.Forms.SizeType>」を参照してください。

8. 行または列を削除するには、[**削除**] ボタンをクリックして、**メンバー**リストで現在選択されているアイテムを削除します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.SizeType>
- [TableLayoutPanel コントロール](tablelayoutpanel-control-windows-forms.md)
