---
title: '方法: コンカレンシーの競合のチェックを指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c2547fcb-58eb-4377-9948-1b8d76a0f3d7
ms.openlocfilehash: fd3db5eb5dc9b74d8ea33af56dd522cf2f3fecdb
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781588"
---
# <a name="how-to-specify-concurrency-conflict-checking"></a>方法: コンカレンシーの競合のチェックを指定する
<xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出すときにコンカレンシーの競合をチェックするデータベース列を指定できます。 詳細については、[コンカレンシーの競合を検査するメンバーを指定する](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、更新の確認時に `HomePage` メンバーを検査しないことを指定しています。 詳細については、「<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>」を参照してください。  
  
 [!code-csharp[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.mapping.updatecheck/cs/northwind.cs#1)]
 [!code-vb[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.mapping.updatecheck/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
