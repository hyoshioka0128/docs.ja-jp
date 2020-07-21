---
title: '方法: PrintTickets を検証およびマージする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- merging PrintTickets [WPF]
- PrintTicket [WPF], merging
- validation of PrintTickets [WPF]
- PrintTicket [WPF], validation
ms.assetid: 4fe2d501-d0b0-4fef-86af-6ffe6c162532
ms.openlocfilehash: bd7f399555b343a52ec6f36aa3b8c706747d8b06
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77094528"
---
# <a name="how-to-validate-and-merge-printtickets"></a>方法: PrintTickets を検証およびマージする
Microsoft Windows の[印刷スキーマ](/windows/win32/printdocs/printschema)には、柔軟で拡張可能な <xref:System.Printing.PrintCapabilities> および <xref:System.Printing.PrintTicket> 要素が含まれています。 前者では、印刷デバイスの機能の明細を示し、後者では、ドキュメントの特定のシーケンス、個々のドキュメント、または個々のページに関してそれらの機能をデバイスでどのように使用するかを指定します。  
  
 印刷をサポートするアプリケーションの一般的なタスク シーケンスは次のとおりです。  
  
1. プリンターの機能を確認します。  
  
2. それらの機能を使用するように <xref:System.Printing.PrintTicket> を構成します。  
  
3. <xref:System.Printing.PrintTicket> を検証します。  
  
 この記事では、この実行方法について説明します。  
  
## <a name="example"></a>例  
 以下の簡単な例では、プリンターが両面印刷をサポートできるかどうかにのみ関心があります。 主な手順は次のとおりです。  
  
1. <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> メソッドを使用して <xref:System.Printing.PrintCapabilities> オブジェクトを取得します。  
  
2. 必要な機能があるかどうかをテストします。 以下の例では、<xref:System.Printing.PrintCapabilities> オブジェクトの <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> プロパティをテストして、用紙の長辺に沿って "ページめくり" を行って用紙の両面に印刷できるかどうかを確認します。 <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> はコレクションなので、<xref:System.Collections.ObjectModel.ReadOnlyCollection%601> の `Contains` メソッドを使用します。  
  
    > [!NOTE]
    > これは厳密には必要ありません。 以下で使用されている <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> メソッドによって、<xref:System.Printing.PrintTicket> の各要求がプリンターの機能と照合されます。 要求された機能がプリンターでサポートされていない場合、プリンター ドライバーによって、メソッドから返された <xref:System.Printing.PrintTicket> の代替要求が置き換えられます。  
  
3. プリンターで両面印刷がサポートされている場合、このサンプル コードでは両面印刷を要求する <xref:System.Printing.PrintTicket> が作成されます。 ただし、アプリケーションによって、<xref:System.Printing.PrintTicket> 要素で使用可能なすべてのプリンター設定が指定されるわけではありません。 これは、プログラマとプログラム時間の両方の点で無駄です。 代わりに、コードで両面印刷要求のみを設定し、この <xref:System.Printing.PrintTicket> を、既存の完全に構成済みで検証済みの <xref:System.Printing.PrintTicket> (この場合はユーザーの既定値の <xref:System.Printing.PrintTicket>) とマージします。  
  
4. そのため、このサンプルでは、<xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> メソッドを呼び出し、新しい最小の <xref:System.Printing.PrintTicket> をユーザーの既定値の <xref:System.Printing.PrintTicket> とマージします。 その結果、プロパティの 1 つとして新しい <xref:System.Printing.PrintTicket> を含む <xref:System.Printing.ValidationResult> が返されます。  
  
5. 次に、このサンプルでは、新しい <xref:System.Printing.PrintTicket> で両面印刷が要求されることをテストします。 行われる場合、サンプルでは、それがユーザーの新しい既定の印刷チケットになります。 上記の手順 2 が省略され、プリンターが長辺に沿った両面印刷をサポートしていない場合、テストの結果は `false` になります (上記の注を参照してください)。  
  
6. 最後の重要な手順は、<xref:System.Printing.PrintQueue> の <xref:System.Printing.PrintQueue.UserPrintTicket%2A> プロパティへの変更を <xref:System.Printing.PrintQueue.Commit%2A> メソッドを使用してコミットすることです。  
  
 [!code-csharp[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#usingmergeandvalidate)]
 [!code-vb[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#usingmergeandvalidate)]  
  
 この例をすぐにテストできるように、残りの部分を以下に示します。 プロジェクトと名前空間を作成してから、この記事の両方のコード スニペットを名前空間ブロックに貼り付けてください。  
  
 [!code-csharp[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#uiformergeandvalidateptutility)]
 [!code-vb[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#uiformergeandvalidateptutility)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Printing.PrintCapabilities>
- <xref:System.Printing.PrintTicket>
- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
- [印刷スキーマ](/windows/win32/printdocs/printschema)
