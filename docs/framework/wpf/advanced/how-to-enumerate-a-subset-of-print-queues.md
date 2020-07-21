---
title: '方法: 印刷キューのサブセットを列挙する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- enumerating [WPF], subset of print queues
- print queues [WPF], enumerating subset of
ms.assetid: cc4a1b5b-d46f-4c5e-bc26-22c226e4bee0
ms.openlocfilehash: aae41931f012f6d34fc057fdd6ee9fc9baab6e7b
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77094541"
---
# <a name="how-to-enumerate-a-subset-of-print-queues"></a>方法: 印刷キューのサブセットを列挙する
企業全体にわたるプリンター セットを管理する情報技術 (IT) プロフェッショナルが直面する一般的な状況は、特定の特性を持つプリンターの一覧を生成することです。 この機能は、<xref:System.Printing.PrintServer> オブジェクトの <xref:System.Printing.PrintServer.GetPrintQueues%2A> メソッドと <xref:System.Printing.EnumeratedPrintQueueTypes> 列挙体によって提供されています。  
  
## <a name="example"></a>例  
 次の例では、一覧表示する印刷キューの特性を指定するフラグの配列を作成することからコードが始まります。 この例では、プリント サーバーのローカルにインストールされ、共有されている印刷キューを探しています。 <xref:System.Printing.EnumeratedPrintQueueTypes> 列挙体には、他にも多くの可能性があります。  
  
 このコードでは、次に、<xref:System.Printing.PrintServer> から派生したクラスである <xref:System.Printing.LocalPrintServer> オブジェクトを作成します。 ローカル プリント サーバーは、アプリケーションが実行されているコンピューターです。  
  
 最後の重要な手順は、配列を <xref:System.Printing.PrintServer.GetPrintQueues%2A> メソッドに渡すことです。  
  
 最後に、結果がユーザーに表示されます。  
  
 [!code-cpp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CPP/Program.cpp#listsubsetofprintqueues)]
 [!code-csharp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CSharp/Program.cs#listsubsetofprintqueues)]
 [!code-vb[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/visualbasic/program.vb#listsubsetofprintqueues)]  
  
 各印刷キューをステップ実行する `foreach` ループで、さらにスクリーニングを行うようにこの例を拡張することができます。 たとえば、ループで各印刷キューの <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> メソッドを呼び出して、両面印刷がサポートされていないプリンターを除外し、両面印刷の有無について返された値をテストすることができます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
- [Microsoft XPS Document Writer](/windows/win32/printdocs/microsoft-xps-document-writer)
