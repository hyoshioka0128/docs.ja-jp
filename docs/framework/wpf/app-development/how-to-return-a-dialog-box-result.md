---
title: '方法: ダイアログ ボックスの結果を返す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dialog boxes [WPF], returning results
ms.assetid: 4c5cf286-746b-4052-934d-d80cbf8acba3
ms.openlocfilehash: 5e3670006762bcd09634b29314ecf2d05b1a44da
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968230"
---
# <a name="how-to-return-a-dialog-box-result"></a>方法: ダイアログ ボックスの結果を返す
この例では、<xref:System.Windows.Window.ShowDialog%2A> の呼び出しによって開かれたウィンドウのダイアログの結果を取得する方法を示します。  
  
## <a name="example"></a>例  
 ダイアログ ボックスを閉じる前に、その <xref:System.Windows.Window.DialogResult%2A> プロパティを、ユーザーがダイアログ ボックスを閉じた方法を示す <xref:System.Nullable%601><xref:System.Boolean> に設定する必要があります。 この値は <xref:System.Windows.Window.ShowDialog%2A> によって返されます。これにより、クライアントのコードでは、ダイアログ ボックスが閉じられた方法がわかり、それにより結果を処理する方法を決定できます。  
  
> [!NOTE]
> <xref:System.Windows.Window.DialogResult%2A> は、ウィンドウが <xref:System.Windows.Window.ShowDialog%2A> を呼び出すことによって開かれた場合にのみ設定できます。  
  
 [!code-csharp[HOWTOWindowManagementSnippets#GetDialogResultCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#getdialogresultcode)]
 [!code-vb[HOWTOWindowManagementSnippets#GetDialogResultCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#getdialogresultcode)]  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 <xref:System.Windows.Window.ShowDialog%2A> を呼び出すには、すべてのウィンドウとユーザー入力イベントを無制限に使用するためのアクセス許可が必要です。
