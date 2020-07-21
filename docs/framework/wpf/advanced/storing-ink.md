---
title: インクの格納
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ISF (Ink Serialized Format)
- storing ink [WPF]
- ink [WPF], storing
- retrieving ink [WPF]
- Ink Serialized Format (ISF)
ms.assetid: a3f6d16b-d682-4680-9965-907332b4d2b8
ms.openlocfilehash: 4089aa7942105c14eb628c75edb7f53ffacfaeb0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053374"
---
# <a name="storing-ink"></a>インクの格納
<xref:System.Windows.Ink.StrokeCollection.Save%2A> メソッドでは、Ink Serialized Format (ISF) としてインクを格納するためのサポートが提供されます。 <xref:System.Windows.Ink.StrokeCollection> クラスのコンストラクターからは、インク データを読み取るためのサポートが提供されます。  
  
## <a name="ink-storage-and-retrieval"></a>インクの格納と取得  
 このセクションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プラットフォームでインクを格納し、取得する方法について説明します。  
  
 次の例では、[ファイルの保存] ダイアログ ボックスをユーザーに提示し、<xref:System.Windows.Controls.InkCanvas> からファイルにインクを保存するボタンクリック イベント ハンドラーが実装されます。  
  
 [!code-csharp[DigitalInkTopics#12](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#12)]
 [!code-vb[DigitalInkTopics#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#12)]  
  
 次の例では、[ファイルを開く] ダイアログ ボックスをユーザーに提示し、ファイルから <xref:System.Windows.Controls.InkCanvas> 要素にインクを読み込むボタンクリック イベント ハンドラーが実装されます。  
  
 [!code-csharp[DigitalInkTopics#13](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#13)]
 [!code-vb[DigitalInkTopics#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#13)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.InkCanvas>
- [Windows Presentation Foundation](../index.md)
