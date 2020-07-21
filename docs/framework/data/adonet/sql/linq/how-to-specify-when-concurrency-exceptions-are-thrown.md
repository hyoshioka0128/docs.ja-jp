---
title: '方法: コンカレンシー例外をいつスローするかを指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 344ae068-ff63-4a2e-8b00-af22e143675f
ms.openlocfilehash: c0f41d23264bbe5c9130cb5a0b03686331bc92b1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781622"
---
# <a name="how-to-specify-when-concurrency-exceptions-are-thrown"></a>方法: コンカレンシー例外をいつスローするかを指定する
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、オプティミスティック コンカレンシーの競合によってオブジェクトが更新されないときに <xref:System.Data.Linq.ChangeConflictException> 例外がスローされます。 詳細については、「[オプティミスティック コンカレンシー:概要)](optimistic-concurrency-overview.md) の下のステートメントを右クリックします。  
  
 変更内容をデータベースに送信する前に、コンカレンシー例外をどの時点でスローするかを指定できます。  
  
- 例外を最初のエラーの時点でスローします (<xref:System.Data.Linq.ConflictMode.FailOnFirstConflict>)。  
  
- 更新の再試行を決められた回数繰り返し、すべてのエラー情報を集積してから、この情報を例外で報告します (<xref:System.Data.Linq.ConflictMode.ContinueOnConflict>)。  
  
 <xref:System.Data.Linq.ChangeConflictException> 例外がスローされると、例外を通じて <xref:System.Data.Linq.ChangeConflictCollection> コレクションにアクセスできます。 このコレクションを使用して、個々の競合 (それぞれが 1 回の更新失敗に対応する) の詳細情報を取得したり、<xref:System.Data.Linq.ObjectChangeConflict.MemberConflicts%2A> コレクションにアクセスしたりすることができます。 各メンバー競合は、コンカレンシー チェックでエラーになった更新の 1 つのメンバーに対応します。  
  
## <a name="example"></a>例  
 両方の値の例を次のコードに示します。  
  
 [!code-csharp[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/vb/module1.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)
- [データの変更と変更の送信](making-and-submitting-data-changes.md)
