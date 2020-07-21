---
title: '方法: データベース値を維持することで競合を解決する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b475cf72-9e64-4f6e-99c1-af7737bc85ef
ms.openlocfilehash: e42f48a188741c3ddff44f6444fa351192c8175f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793337"
---
# <a name="how-to-resolve-conflicts-by-retaining-database-values"></a>方法: データベース値を維持することで競合を解決する
変更内容を再送信する前に、データベース内の予期した値と実際の値の違いを調整するために、<xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues> を使用することで、データベース内の値を維持できます。 この場合、オブジェクト モデル内の現在の値は上書きされます。 詳しくは、「[オプティミスティック コンカレンシー: 概要)](optimistic-concurrency-overview.md) の下のステートメントを右クリックします。  
  
> [!NOTE]
> どの場合も、データベースから最新のデータを取得することで、まずクライアントのレコードが更新されます。 この処理によって、次の更新処理が同じコンカレンシー チェックで失敗することを防止できます。  
  
## <a name="example"></a>例  
 このシナリオでは、ユーザー 1 が変更内容を送信しようとしたときに <xref:System.Data.Linq.ChangeConflictException> 例外がスローされます。途中でユーザー 2 が Assistant 列と Department  列を変更したためです。 次の表は、この状況を示しています。  
  
||管理者|Assistant|Department|  
|------|-------------|---------------|----------------|  
|ユーザー 1 およびユーザー 2 が照会した最初のデータベース状態|Alfreds|Maria|Sales|  
|ユーザー 1 が送信しようとした変更内容|Alfred||Marketing|  
|ユーザー 2 が既に送信した変更内容||Mary|サービス|  
  
 ユーザー 1 は、この競合を解決するために、新しいデータベース値でオブジェクト モデルの現在の値を上書きすることに決めます。  
  
 ユーザー 1 が <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues> を使用して競合を解決すると、データベース内の結果は次の表のようになります。  
  
||管理者|Assistant|Department|  
|------|-------------|---------------|----------------|  
|競合解決後の新しい状態|Alfreds<br /><br /> (元の値)|Mary<br /><br /> (ユーザー 2 の値)|サービス<br /><br /> (ユーザー 2 の値)|  
  
 オブジェクト モデルの現在の値をデータベース値で上書きする方法を次のコード例に示します  (個々のメンバーの競合に対する検査やカスタム ハンドリングは行われません)。  
  
 [!code-csharp[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)
