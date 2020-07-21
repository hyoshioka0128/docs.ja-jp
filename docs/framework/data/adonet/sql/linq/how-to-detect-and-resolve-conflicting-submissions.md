---
title: '方法: 送信の競合を検出および解決する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 91e27206-01fb-4c7a-8afc-1383a6ac5067
ms.openlocfilehash: 2de0182cc0b87768a9cff553b7ec6e77f8ccc7b8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793775"
---
# <a name="how-to-detect-and-resolve-conflicting-submissions"></a>方法: 送信の競合を検出および解決する
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] には、複数のユーザーがデータベースを変更するために生じる競合を、検出および解決するための多くのリソースが用意されています。 詳細については、[変更の競合を管理する](how-to-manage-change-conflicts.md)」を参照してください。  
  
## <a name="example"></a>例  
 <xref:System.Data.Linq.ChangeConflictException> 例外をキャッチする `try`/`catch` ブロックの例を次にします。 各競合のエンティティおよびメンバー情報が、コンソール ウィンドウに表示されます。  
  
> [!NOTE]
> 情報の取得をサポートするには、`using System.Reflection` ディレクティブ (Visual Basic の場合は `Imports System.Reflection`) を含める必要があります。 詳細については、「<xref:System.Reflection>」を参照してください。  
  
 [!code-csharp[DLinqSubmittingChanges#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#2)]
 [!code-vb[DLinqSubmittingChanges#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [データの変更と変更の送信](making-and-submitting-data-changes.md)
- [方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)
