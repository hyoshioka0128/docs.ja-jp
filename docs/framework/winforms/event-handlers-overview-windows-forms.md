---
title: イベント ハンドラーの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, event handling
- event handling [Windows Forms], Windows Forms
- event handlers [Windows Forms], about event handlers
ms.assetid: 228112e1-1711-42ee-8ffa-ff3555bffe66
ms.openlocfilehash: ffec8a9f8e080dec78152e62e00e2dceefbdaab0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141693"
---
# <a name="event-handlers-overview-windows-forms"></a>イベント ハンドラーの概要 (Windows フォーム)
イベント ハンドラーは、イベントにバインドされるメソッドです。 イベントが発生すると、イベント ハンドラー内のコードが実行されます。 各イベント ハンドラーには、イベントを適切に処理するための 2 つのパラメーターが用意されています。 コントロールのイベント ハンドラーの例を<xref:System.Windows.Forms.Button>次に<xref:System.Windows.Forms.Control.Click>示します。  
  
```vb  
Private Sub button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles button1.Click  
  
End Sub  
```  
  
```csharp  
private void button1_Click(object sender, System.EventArgs e)
{  
  
}  
```  
  
```cpp  
private:  
  void button1_Click(System::Object ^ sender,  
    System::EventArgs ^ e)  
  {  
  
  }  
```  
  
 最初のパラメーター`sender`は、イベントを発生させたオブジェクトへの参照を提供します。 2 番目の`e`パラメータは、上の例では、処理されるイベントに固有のオブジェクトを渡します。 オブジェクトのプロパティ (および場合によってはメソッド) を参照することにより、マウス イベントのマウスの位置やドラッグ アンド ドロップ イベントで転送されるデータなどの情報を取得できます。  
  
 通常、各イベントは、2 番目のパラメーターに対して異なるイベント オブジェクト型を持つイベント ハンドラーを生成します。 イベントと イベントのイベント ハンドラーなど<xref:System.Windows.Forms.Control.MouseDown>、2 番目の<xref:System.Windows.Forms.Control.MouseUp>パラメーターに対して同じオブジェクト型を持つイベント ハンドラーもあります。 これらの種類のイベントでは、同じイベント ハンドラーを使用して両方のイベントを処理できます。  
  
 同じイベント ハンドラーを使用して、異なるコントロールに対して同じイベントを処理することもできます。 たとえば、フォーム上にコントロールの<xref:System.Windows.Forms.RadioButton>グループがある場合、イベントに対して 1 つのイベント ハンドラーを<xref:System.Windows.Forms.Control.Click>作成し、各コントロールの<xref:System.Windows.Forms.Control.Click>イベントを 1 つのイベント ハンドラーにバインドできます。 詳細については、「[方法 : Windows フォームで複数のイベントを 1 つのイベント ハンドラに接続する](how-to-connect-multiple-events-to-a-single-event-handler-in-windows-forms.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Windows フォーム内でのイベント ハンドラーの作成](creating-event-handlers-in-windows-forms.md)
- [イベントの概要](events-overview-windows-forms.md)
