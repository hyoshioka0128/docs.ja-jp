---
title: '方法: イメージを持つ Button を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Button controls [WPF], creating
ms.assetid: 607a193c-4098-4dd8-8dc0-51256cec2020
ms.openlocfilehash: 5be928ac75ad727feabcde07ac0c6dc76ed130e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910950"
---
# <a name="how-to-create-a-button-that-has-an-image"></a>方法: イメージを持つ Button を作成する
この例では、<xref:System.Windows.Controls.Button> でイメージを含める方法を示します。  
  
## <a name="example"></a>例  
 次の例では、2 つの <xref:System.Windows.Controls.Button> コントロールが作成されます。 一方の <xref:System.Windows.Controls.Button> にはテキストが含まれ、もう一方にはイメージが含まれます。 イメージはデータという名称のフォルダーに入ります。このフォルダーは、例のプロジェクト フォルダーのサブフォルダーです。 イメージが含まれる <xref:System.Windows.Controls.Button> をユーザーがクリックすると、他の <xref:System.Windows.Controls.Button> の背景とテキストが変わります。  
  
 この例では、マークアップを利用して <xref:System.Windows.Controls.Button> コントロールが作成されますが、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーの記述にはコードが使用されています。  
  
 [!code-xaml[BtnColor#4](~/samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml#4)]  
  
 [!code-csharp[BtnColor#6](~/samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml.cs#6)]
 [!code-vb[BtnColor#6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BtnColor/VisualBasic/Pane1.xaml.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [コントロール](index.md)
- [コントロール ライブラリ](control-library.md)
