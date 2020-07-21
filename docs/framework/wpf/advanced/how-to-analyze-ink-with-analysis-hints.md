---
title: '方法: 分析のヒントに従ってインクを分析する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ink [WPF], analyzing
- analyzing ink [WPF]
- ink [WPF], AnalysisHintNode objects [WPF]
- AnalysisHintNode objects [WPF]
ms.assetid: d4421ed4-77f5-4640-829e-9f1de50b2ff2
ms.openlocfilehash: a4c38ddf52e9054fe9126df4b7e172548617b90d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777001"
---
# <a name="how-to-analyze-ink-with-analysis-hints"></a>方法: 分析のヒントに従ってインクを分析する
[System.Windows.Ink.AnalysisHintNode](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms610344(v=vs.90)) では、それがアタッチされている [System.Windows.Ink.InkAnalyzer](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms616754(v=vs.90)) にヒントを指定できます。  このヒントは、[System.Windows.Ink.AnalysisHintNode](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms610344(v=vs.90)) の [System.Windows.Ink.ContextNode.Location%2A](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms594508(v=vs.90)) プロパティで指定した領域に適用され、インク アナライザーに追加のコンテキストを提供して認識精度を向上させます。 このコンテンツ情報は、[System.Windows.Ink.InkAnalyzer](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms616754(v=vs.90)) がヒント領域から得たインクを分析するときに適用されます。  
  
## <a name="example"></a>例  
 次の例では、フォームで [System.Windows.Ink.AnalysisHintNode](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms610344(v=vs.90)) オブジェクトが複数使用される、インク入力を取るアプリケーションを示しています。 このアプリケーションでは、[System.Windows.Ink.AnalysisHintNode.Factoid%2A](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms594341(v=vs.90)) プロパティを使用して、フォーム上の各エントリに対してコンテキスト情報を提供します。  このアプリケーションでは、バックグラウンド分析を使用してインクを分析し、ユーザーがインクの追加を停止してから 5 秒後にフォームからすべてのインクがクリアされます。  
  
 [!code-xaml[HowToAnalyzeInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml#1)]  
  
 [!code-csharp[HowToAnalyzeInk#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml.cs#2)]
 [!code-vb[HowToAnalyzeInk#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToAnalyzeInk/VisualBasic/FormAnalyzer.xaml.vb#2)]
