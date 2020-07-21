---
title: '方法: クロックを同期的にシークする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clocks [WPF], seeking synchronously
- seeking clocks synchronously [WPF]
ms.assetid: e5b7529b-b7d0-40d2-9e1d-fa4b5e736e96
ms.openlocfilehash: 9b6b1f5523effc56ccd9ddaa4f478e1d3a20ada8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651260"
---
# <a name="how-to-seek-a-clock-synchronously"></a>方法: クロックを同期的にシークする
<xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A> メソッドを使用して、特定のポイントまでクロックを同期的にシークします。 次の例は、<xref:System.Windows.Media.Animation.ClockController> の <xref:System.Windows.Media.Animation.ClockController.Seek%2A> メソッドと <xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A> メソッドの両方を示しています。  
  
 この例は、<xref:System.Windows.Media.Animation.Clock> をシークする方法を示します。ストーリーボードをシークする方法の例については、「[ストーリーボードを同期的にシークする](how-to-seek-a-storyboard-synchronously.md)」を参照してください。  
  
## <a name="example"></a>例  
 [!code-csharp[ClockController_procedural_snip#ClockControllerSeekExample](~/samples/snippets/csharp/VS_Snippets_Wpf/ClockController_procedural_snip/CSharp/SeekAlignedToLastTickExample.cs#clockcontrollerseekexample)]
 [!code-vb[ClockController_procedural_snip#ClockControllerSeekExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClockController_procedural_snip/visualbasic/seekalignedtolasttickexample.vb#clockcontrollerseekexample)]
