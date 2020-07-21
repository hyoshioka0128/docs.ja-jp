---
title: '方法: 変更セットを表示する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 126e7245-c5a0-4ebf-800d-cc1fcf9cd0ab
ms.openlocfilehash: 5f49e123e6e980501d330eeecf2719023cdff8e7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781967"
---
# <a name="how-to-display-a-changeset"></a>方法: 変更セットを表示する
<xref:System.Data.Linq.DataContext> によって追跡される変更を <xref:System.Data.Linq.DataContext.GetChangeSet%2A> を使って表示することができます。  
  
## <a name="example"></a>例  
 以下の例では、住所がロンドンの顧客を取得し、これをパリに変更してから変更内容をデータベースに送信しています。  
  
 [!code-csharp[DLinqDebuggingSupport#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDebuggingSupport/cs/Program.cs#2)]
 [!code-vb[DLinqDebuggingSupport#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDebuggingSupport/vb/Module1.vb#2)]  
  
 このコードからの出力は次のようになります。 最後に概要として、8 か所の変更が示されることに注意してください。  

 ```console
CustomerID: AROUT
   Original value: London
   Updated value: Paris
CustomerID: BSBEV
   Original value: London
   Updated value: Paris
CustomerID: CONSH
   Original value: London
   Updated value: Paris
CustomerID: EASTC
   Original value: London
   Updated value: Paris
CustomerID: NORTS
    Original value: London
    Updated value: Paris
CustomerID: PARIS
    Original value: London
    Updated value: Paris
CustomerID: SEVES
    Original value: London
    Updated value: Paris
CustomerID: SPECD
    Original value: London
    Updated value: Paris
Total changes: {Added: 0, Removed: 0, Modified: 8}
```
  
## <a name="see-also"></a>関連項目

- [デバッグのサポート](debugging-support.md)
