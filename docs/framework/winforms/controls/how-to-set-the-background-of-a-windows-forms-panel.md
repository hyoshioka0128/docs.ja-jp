---
title: パネルの背景を設定する
description: デザイナーを使用して、Windows フォームパネルの背景色と背景イメージを設定する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- background colors [Windows Forms], Windows Forms Panel controls
- background images [Windows Forms], Windows Forms Panel controls
- Panel control [Windows Forms], background
- colors [Windows Forms], Windows Forms Panel controls
ms.assetid: 096cbd8d-45cc-47b8-b1ef-a27f60ea8be0
ms.openlocfilehash: 109ff6184de9c79d1576207bbeb29ad939670b6f
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173381"
---
# <a name="how-to-set-the-background-of-a-windows-forms-panel"></a>方法 : Windows フォーム パネルの背景を設定する
Windows フォームコントロールには、 <xref:System.Windows.Forms.Panel> 背景色と背景画像の両方を表示できます。 プロパティは、 <xref:System.Windows.Forms.Control.BackColor%2A> ラベルやラジオボタンなど、含まれるコントロールの背景色を設定します。 <xref:System.Windows.Forms.Control.BackgroundImage%2A>プロパティが設定されていない場合、 <xref:System.Windows.Forms.Control.BackColor%2A> パネル全体が選択されます。 プロパティが設定されている場合、イメージは、 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 含まれているコントロールの背後に表示されます。  
  
### <a name="to-set-the-background-programmatically"></a>バックグラウンドをプログラムによって設定するには  
  
1. パネルの <xref:System.Windows.Forms.Control.BackColor%2A> プロパティを型の値に設定 <xref:System.Drawing.Color?displayProperty=nameWithType> します。  
  
    ```vb  
    Panel1.BackColor = Color.AliceBlue  
    ```  
  
    ```csharp  
    panel1.BackColor = Color.AliceBlue;  
    ```  
  
    ```cpp  
    panel1->BackColor = Color::AliceBlue;  
    ```  
  
2. <xref:System.Windows.Forms.Control.BackgroundImage%2A>クラスのメソッドを使用して、パネルのプロパティを設定し <xref:System.Drawing.Image.FromFile%2A> <xref:System.Drawing.Image?displayProperty=nameWithType> ます。  
  
    ```vb  
    ' You should replace the bolded image
    ' in the sample below with an image of your own choosing.  
    Panel1.BackgroundImage = Image.FromFile _  
        (System.Environment.GetFolderPath _  
        (System.Environment.SpecialFolder.Personal) _  
        & "\Image.gif")  
    ```  
  
    ```csharp  
    // You should replace the bolded image
    // in the sample below with an image of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    panel1.BackgroundImage = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
    ```  
  
    ```cpp  
    // You should replace the bolded image
    // in the sample below with an image of your own choosing.  
    panel1->BackgroundImage = Image::FromFile(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\Image.gif"));  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Control.BackColor%2A>
- <xref:System.Windows.Forms.Control.BackgroundImage%2A>
- [Panel コントロール](panel-control-windows-forms.md)
- [Panel コントロールの概要](panel-control-overview-windows-forms.md)
