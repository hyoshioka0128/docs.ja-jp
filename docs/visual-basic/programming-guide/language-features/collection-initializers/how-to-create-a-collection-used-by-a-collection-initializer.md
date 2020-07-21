---
title: '方法: コレクション初期化子によって使用されるコレクションを作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- collection initializers [Visual Basic]
ms.assetid: c858db10-424d-47e0-92cd-e08087cc5ebc
ms.openlocfilehash: 7cba290b92f41125a93d1ed022e4db5ef62da789
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414557"
---
# <a name="how-to-create-a-collection-used-by-a-collection-initializer-visual-basic"></a>方法: コレクション初期化子を使用してコレクションを作成する (Visual Basic)
コレクション初期化子を使用してコレクションを作成すると、`Add` メソッドのパラメーターがコレクション初期化子の値の型と一致するコレクション型の `Add` メソッドが、Visual Basic コンパイラによって検索されます。 この `Add` メソッドは、コレクションに、コレクション初期化子の値を設定するときに使用されます。  
  
## <a name="example"></a>例  
 次の例が示す `OrderCollection` コレクションにはパブリック `Add` メソッドが含まれています。このメソッドは、コレクション初期化子が `Order` 型のオブジェクトを追加するときに使用できます。 `Add` メソッドを使用すると、短縮されたコレクション初期化子構文を使用できます。  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#4)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#2)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [コレクション初期化子](index.md)
- [方法: コレクション初期化子によって使用される Add 拡張メソッドを作成する](how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)
