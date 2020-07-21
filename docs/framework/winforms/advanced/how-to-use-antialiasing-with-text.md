---
title: '方法: テキストでのアンチエイリアシングの使用'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [Windows Forms], smoothing drawn
- antialiasing [Windows Forms], using with text
- text [Windows Forms], smoothing
- text [Windows Forms], antialiasing
- strings [Windows Forms], antialiasing when drawing
ms.assetid: 48fc34f3-f236-4b01-a0cb-f0752e6d22ae
ms.openlocfilehash: 632ed329173d134495a424b34ca7c71e402607bf
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182482"
---
# <a name="how-to-use-antialiasing-with-text"></a>方法: テキストでのアンチエイリアシングの使用
*アンチエイリアシング*とは、描画されたグラフィックスとテキストのギザギザのエッジをスムージングして、外観や読みやすさを向上させます。 マネージ GDI+ クラスを使用すると、高品質のアンチエイリアステキストをレンダリングできるだけでなく、低品質のテキストをレンダリングできます。 通常、高品質のレンダリングは、低品質のレンダリングよりも処理に時間がかかります。 テキストの品質レベルを設定するには、列挙<xref:System.Drawing.Graphics.TextRenderingHint%2A>体の要素<xref:System.Drawing.Graphics>の 1 つに a<xref:System.Drawing.Text.TextRenderingHint>のプロパティを設定します。  
  
## <a name="example"></a>例  
 次のコード例では、2 つの異なる品質設定を使用してテキストを描画します。  
  
 [!code-csharp[System.Drawing.FontsAndText#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.FontsAndText#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#21)]  

 次の図は、コード例の出力を示しています。  
  
 ![2 つの異なる品質設定を持つテキストを示すスクリーンショット。](./media/how-to-use-antialiasing-with-text/antialiasing-text-quality-settings.png)  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記のコード例は Windows フォームで使用するように設計されており、<xref:System.Windows.Forms.PaintEventArgs>`e`のパラメーターである が必要<xref:System.Windows.Forms.PaintEventHandler>です。  
  
## <a name="see-also"></a>関連項目

- [フォントとテキストの使用](using-fonts-and-text.md)
