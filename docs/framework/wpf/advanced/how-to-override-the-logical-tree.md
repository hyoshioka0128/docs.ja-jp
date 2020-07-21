---
title: '方法: 論理ツリーをオーバーライドする'
ms.date: 03/30/2017
helpviewer_keywords:
- overriding the logical tree [WPF]
- logical tree [WPF], overriding
ms.assetid: 0ae4d074-8113-4b06-b4fa-e0f39d4967a6
ms.openlocfilehash: bf3459fff1a90326794d6713dd39c73596b0e960
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768447"
---
# <a name="how-to-override-the-logical-tree"></a>方法: 論理ツリーをオーバーライドする
ほとんどの場合は必要ありませんが、高度なコントロールを作成する場合は、必要に応じて論理ツリーをオーバーライドできます。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.StackPanel> をサブクラス化して論理ツリーをオーバーライドする方法を次の例に示します。この例では、パネルが子要素を 1 つだけ持つことができ、その子要素だけをレンダリングするという動作を強制的に適用しています。 これは実際的には必ずしも好ましい動作ではありませんが、ここでは要素の通常の論理ツリーをオーバーライドするシナリオを説明するための手段として示します。  
  
 [!code-csharp[LogicalOverride#SingletonPanel](~/samples/snippets/csharp/VS_Snippets_Wpf/LogicalOverride/CSharp/SDKSampleLibrary/class1.cs#singletonpanel)]  
  
 論理ツリーについて詳しくは、「[WPF のツリー](trees-in-wpf.md)」をご覧ください。
