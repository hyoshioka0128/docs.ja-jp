---
title: '方法: 遅延読み込みをオフにする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1b84b852-3cad-41a7-8077-149a70d50c8b
ms.openlocfilehash: 6559392527bb02afe9cea61e704f1f371c6d5470
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781657"
---
# <a name="how-to-turn-off-deferred-loading"></a>方法: 遅延読み込みをオフにする
<xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> を `false` に設定すると、遅延読み込みをオフにできます。 詳細については、「[遅延読み込みと即時読み込み](deferred-versus-immediate-loading.md)」を参照してください。  
  
> [!NOTE]
> 遅延読み込みは、オブジェクト トラッキングをオフにすると暗黙でオフになります。 詳細については、[情報を読み取り専用として取得する](how-to-retrieve-information-as-read-only.md)」を参照してください。  
  
## <a name="example"></a>例  
 <xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> を `false` に設定して、遅延読み込みをオフにする方法を次の例に示します。  
  
 [!code-csharp[DLinqQuerying#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#3)]
 [!code-vb[DLinqQuerying#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [クエリの概念](query-concepts.md)
- [データベースに対するクエリの実行](querying-the-database.md)
