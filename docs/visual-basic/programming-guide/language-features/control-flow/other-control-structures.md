---
title: その他の制御構造
ms.date: 07/20/2015
helpviewer_keywords:
- statements [Visual Basic], control flow
- control structures [Visual Basic]
ms.assetid: 24b811f7-98ba-40ec-8dd3-4d528cfa4574
ms.openlocfilehash: c6d80b237c7c3512c2904547842fdeb3c69bef68
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402019"
---
# <a name="other-control-structures-visual-basic"></a>その他の制御構造 (Visual Basic)
Visual Basic には、リソースを破棄したり、オブジェクト参照を繰り返さなければならない回数を減らしたりするうえで役立つ制御構造が用意されています。  
  
## <a name="usingend-using-construction"></a>Using...End Using コンストラクション  
 `Using...End Using` コンストラクションによりステートメント ブロックが構築され、このブロック内で SQL 接続などのリソースを使用します。 必要に応じて、`Using` ステートメントを使用してリソースを取得できます。 `Using` ブロックを終了すると、リソースが自動的に破棄され、他のコードがそのリソースを使用できるようになります。 リソースはローカルで、破棄可能である必要があります。 詳細については、「[Using ステートメント](../../../language-reference/statements/using-statement.md)」を参照してください。  
  
## <a name="withend-with-construction"></a>With...End With コンストラクション  
 `With...End With` コンストラクションを使用すると、オブジェクト参照を一度指定した後、そのメンバーにアクセスする一連のステートメントを実行できます。 これにより、Visual Basic にアクセスするステートメントごとに参照を再確立する必要がなくなるため、コードが簡略化され、パフォーマンスが向上します。 詳細については、「[With...End With ステートメント](../../../language-reference/statements/with-end-with-statement.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [制御フロー](index.md)
- [条件判断構造](decision-structures.md)
- [ループ構造](loop-structures.md)
- [入れ子になった制御構造](nested-control-structures.md)
- [Using ステートメント](../../../language-reference/statements/using-statement.md)
- [With...End With ステートメント](../../../language-reference/statements/with-end-with-statement.md)
