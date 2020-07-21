---
title: '方法: アプリケーション ジェスチャを認識する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application gestures [WPF], recognizing
- gestures [WPF], recognizing
ms.assetid: d58b740f-5192-4a3e-af59-7aa162e6ca15
ms.openlocfilehash: 647e7c9c1d785cebfdc362dc48511d865f3945dc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768434"
---
# <a name="how-to-recognize-application-gestures"></a>方法: アプリケーション ジェスチャを認識する
次の例からは、ユーザーが <xref:System.Windows.Controls.InkCanvas> で <xref:System.Windows.Ink.ApplicationGesture.ScratchOut> ジェスチャをしたときにインクを消す方法がわかります。 この例では、`inkCanvas1` という名称の <xref:System.Windows.Controls.InkCanvas> が XAML ファイルで宣言されているものと想定します。  
  
## <a name="example"></a>例  
 [!code-csharp[HowToRecognizeGestures#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToRecognizeGestures/CSharp/Window1.xaml.cs#1)]
 [!code-vb[HowToRecognizeGestures#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToRecognizeGestures/VisualBasic/Window1.xaml.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Ink.ApplicationGesture>
- <xref:System.Windows.Controls.InkCanvas>
- <xref:System.Windows.Controls.InkCanvas.Gesture>
