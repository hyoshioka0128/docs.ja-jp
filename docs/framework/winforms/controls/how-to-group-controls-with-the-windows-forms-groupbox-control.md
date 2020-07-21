---
title: GroupBox コントロールを使用したコントロールのグループ化
description: 関連する要素の視覚的なグループを作成できるように、Windows フォーム GroupBox コントロールを使用してコントロールをグループ化する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], grouping
- GroupBox control [Windows Forms], grouping controls
- Windows Forms controls, grouping
ms.assetid: 0bda316d-bd2a-43aa-ac73-342453303169
ms.openlocfilehash: f84c495a18f4ae5e04367f024a1e2849f1ed59f9
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618065"
---
# <a name="how-to-group-controls-with-the-windows-forms-groupbox-control"></a>方法: Windows フォーム GroupBox コントロールを使用してコントロールをグループ化する
Windows フォーム <xref:System.Windows.Forms.GroupBox> コントロールは、他のコントロールをグループ化するために使用されます。 コントロールをグループ化する理由は3つあります。  
  
- クリアユーザーインターフェイスに関連するフォーム要素の視覚的なグループ化を作成するには  
  
- プログラムによるグループ化 (オプションボタンなど) を作成する場合は。  
  
- デザイン時にコントロールを1つの単位として移動する場合は。  
  
### <a name="to-create-a-group-of-controls"></a>コントロールのグループを作成するには  
  
1. <xref:System.Windows.Forms.GroupBox>フォーム上にコントロールを描画します。  
  
2. グループボックスに他のコントロールを追加し、それぞれをグループボックス内に描画します。  
  
     グループボックスに含める既存のコントロールがある場合は、すべてのコントロールを選択してクリップボードに <xref:System.Windows.Forms.GroupBox> 貼り付け、コントロールを選択して、グループボックスに貼り付けることができます。 また、[グループ] ボックスにドラッグすることもできます。  
  
3. <xref:System.Windows.Forms.GroupBox.Text%2A>グループボックスのプロパティを適切なキャプションに設定します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.GroupBox>
- [GroupBox コントロール](groupbox-control-windows-forms.md)
