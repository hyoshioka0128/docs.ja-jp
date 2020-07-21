---
title: Set RadioButton コントロールをセットとして機能するようにグループ化する
description: 他のセットとは独立して機能するように Windows フォーム RadioButton コントロールをグループ化する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- radio buttons [Windows Forms], grouping
- controls [Windows Forms], grouping
- Windows Forms controls, grouping
- RadioButton control [Windows Forms], grouping
ms.assetid: 58f8fe34-50b7-49d8-a2be-c271be3c6b32
ms.openlocfilehash: 9f6795330922e739cca1f2b5c11bb2ec68bb4e84
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325921"
---
# <a name="how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set"></a>方法: セットとして機能する Windows フォーム RadioButton コントロールをグループ化する
Windows フォーム <xref:System.Windows.Forms.RadioButton> コントロールは、ユーザーが2つ以上の設定を選択できるように設計されており、1つのプロシージャまたはオブジェクトに割り当てることができるのは1つだけです。 たとえば、コントロールのグループでは、 <xref:System.Windows.Forms.RadioButton> 注文に対して選択されたパッケージキャリアを表示できますが、使用されるのは1つの配送業者だけです。 そのため <xref:System.Windows.Forms.RadioButton> 、機能グループの一部であっても、一度に1つだけ選択できます。  
  
 ラジオボタンをグループ化するには、コントロール、コントロール、フォームなどのコンテナー内にオプションボタンを描画し <xref:System.Windows.Forms.Panel> <xref:System.Windows.Forms.GroupBox> ます。 フォームに直接追加されたすべてのラジオボタンは、1つのグループになります。 個別のグループを追加するには、パネルまたはグループボックス内に配置する必要があります。 パネルまたはグループボックスの詳細については、「 [Panel コントロールの概要](panel-control-overview-windows-forms.md)」または「 [GroupBox コントロールの概要](groupbox-control-overview-windows-forms.md)」を参照してください。  
  
### <a name="to-group-radiobutton-controls-as-a-set-to-function-independently-of-other-sets"></a>RadioButton コントロールを他のセットとは独立して機能するようにグループ化するには  
  
1. <xref:System.Windows.Forms.GroupBox> <xref:System.Windows.Forms.Panel> **ツールボックス**の [ **Windows フォーム**] タブからコントロールまたはコントロールをフォームにドラッグします。  
  
2. コントロール <xref:System.Windows.Forms.RadioButton> またはコントロールにコントロールを描画 <xref:System.Windows.Forms.GroupBox> <xref:System.Windows.Forms.Panel> します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.RadioButton>
- [RadioButton コントロールの概要](radiobutton-control-overview-windows-forms.md)
- [Panel コントロールの概要](panel-control-overview-windows-forms.md)
- [GroupBox コントロールの概要](groupbox-control-overview-windows-forms.md)
- [CheckBox コントロールの概要](checkbox-control-overview-windows-forms.md)
- [RadioButton コントロール](radiobutton-control-windows-forms.md)
