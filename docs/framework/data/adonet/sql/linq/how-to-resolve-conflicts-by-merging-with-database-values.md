---
title: '方法: データベース値とマージすることで競合を解決する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1988b79c-3bfc-4c5c-a08a-86cf638bbe17
ms.openlocfilehash: 18a7eceeec63d9caadefab8d98942f10d82c99ca
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793351"
---
# <a name="how-to-resolve-conflicts-by-merging-with-database-values"></a>方法: データベース値とマージすることで競合を解決する
変更内容を再送信する前に、データベース内の予期した値と実際の値の違いを調整するために、<xref:System.Data.Linq.RefreshMode.KeepChanges> を使用して、データベース内の値を現在のクライアント メンバー値とマージできます。 詳しくは、「[オプティミスティック コンカレンシー: 概要)](optimistic-concurrency-overview.md) の下のステートメントを右クリックします。  
  
> [!NOTE]
> どの場合も、データベースから最新のデータを取得することで、まずクライアントのレコードが更新されます。 この処理によって、次の更新処理が同じコンカレンシー チェックで失敗することを防止できます。  
  
## <a name="example"></a>例  
 このシナリオでは、ユーザー 1 が変更内容を送信しようとしたときに <xref:System.Data.Linq.ChangeConflictException> 例外がスローされます。途中でユーザー 2 が Assistant 列と Department  列を変更したためです。 次の表は、この状況を示しています。  
  
||管理者|Assistant|Department|  
|------|-------------|---------------|----------------|  
|ユーザー 1 およびユーザー 2 が照会した最初のデータベース状態|Alfreds|Maria|Sales|  
|ユーザー 1 が送信しようとした変更内容|Alfred||Marketing|  
|ユーザー 2 が既に送信した変更内容||Mary|サービス|  
  
 ユーザー 1 は、この競合を解決するために、データベース値を現在のクライアント メンバー値にマージすることに決めます。 その結果、現在の変更セットでも値が変更されているデータベース値のみが上書きされます。  
  
 ユーザー 1 が <xref:System.Data.Linq.RefreshMode.KeepChanges> を使用して競合を解決すると、データベース内の結果は次の表のようになります。  
  
||管理者|Assistant|Department|  
|------|-------------|---------------|----------------|  
|競合解決後の新しい状態|Alfred<br /><br /> (ユーザー 1 の値)|Mary<br /><br /> (ユーザー 2 の値)|Marketing<br /><br /> (ユーザー 1 の値)|  
  
 次の例では、クライアントでも値が変更されている場合を除き、データベース値を現在のクライアント メンバー値にマージする方法を示しています。 個別のメンバーの競合に対する検査やカスタム ハンドリングは発生しません。  
  
 [!code-csharp[System.Data.Linq.RefreshMode#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#3)]
 [!code-vb[System.Data.Linq.RefreshMode#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [方法: データベース値を上書きすることで競合を解決する](how-to-resolve-conflicts-by-overwriting-database-values.md)
- [方法: データベース値を維持することで競合を解決する](how-to-resolve-conflicts-by-retaining-database-values.md)
- [方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)
