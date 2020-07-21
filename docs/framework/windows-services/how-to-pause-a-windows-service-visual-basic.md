---
title: '方法: Windows サービスを一時中断する (Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
f1_keywords:
- ServiceController.Pause
helpviewer_keywords:
- Windows Service applications, pausing
- pausing Windows Service applications
ms.assetid: eddb9409-942b-46b6-a2ce-fbd4c65f2790
author: ghogen
ms.openlocfilehash: 166eda4a9348188fa6e5048fd3ce41645cde4816
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053599"
---
# <a name="how-to-pause-a-windows-service-visual-basic"></a>方法: Windows サービスを一時中断する (Visual Basic)
この例では、<xref:System.ServiceProcess.ServiceController> コンポーネントを使って、ローカル コンピューター上の IIS 管理サービスを一時停止します。  
  
## <a name="example"></a>例  
 [!code-vb[VbRadconService#11](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#11)]  
[!code-vb[VbRadconService#12](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#12)]  
  
 このコード例は、IntelliSense コード スニペットとしても利用できます。 コード スニペット ピッカーでは、これは **[Windows オペレーティング システム] > [Windows サービス]** に配置されます。 詳細については、「[Code Snippets](/visualstudio/ide/code-snippets)」を参照してください。  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- System.serviceprocess.dll へのプロジェクト参照が必要です。  
  
- <xref:System.ServiceProcess> 名前空間のメンバーへのアクセス許可。 コード内でメンバー名を完全修飾していない場合は、`Imports` ステートメントを追加します。 詳細については、「[Imports ステートメント (.NET 名前空間および型)](../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)」を参照してください。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 <xref:System.ServiceProcess.ServiceController> クラスの <xref:System.ServiceProcess.ServiceController.MachineName%2A> プロパティは、既定ではローカル コンピューターです。 別のコンピューター上の Windows サービスを参照するには、<xref:System.ServiceProcess.ServiceController.MachineName%2A> プロパティをそのコンピューターの名前に変更します。  
  
 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- サービスを一時停止できません。 (<xref:System.InvalidOperationException>)  
  
- システム API にアクセス中にエラーが発生しました。 (<xref:System.ComponentModel.Win32Exception>)  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 コンピューター上のサービスの制御は、<xref:System.ServiceProcess.ServiceControllerPermissionAccess> を使って <xref:System.ServiceProcess.ServiceControllerPermission> のアクセス許可を設定することにより制限できます。  
  
 サービス情報へのアクセスは、<xref:System.Security.Permissions.PermissionState> を使って <xref:System.Security.Permissions.SecurityPermission> のアクセス許可を設定することにより制限できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceProcess.ServiceController>
- <xref:System.ServiceProcess.ServiceControllerStatus>
- <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A>
- [方法: Windows サービスを続行する (Visual Basic)](how-to-continue-a-windows-service-visual-basic.md)
