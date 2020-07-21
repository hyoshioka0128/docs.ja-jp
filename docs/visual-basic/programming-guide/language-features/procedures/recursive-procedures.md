---
title: 再帰プロシージャ
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], that call themselves
- procedures [Visual Basic], recursive
- procedures [Visual Basic], calling
- recursive procedures
- functions [Visual Basic], calling recursively
- recursion
ms.assetid: ba1d3962-b4c3-48d3-875e-96fdb4198327
ms.openlocfilehash: 646d4e29ed7a0b6367d4b35a7f8641bcf659e616
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352552"
---
# <a name="recursive-procedures-visual-basic"></a>再帰プロシージャ (Visual Basic)

"*再帰*" プロシージャとは、自身を呼び出すプロシージャです。 一般に、これは Visual Basic コードを記述する最も効果的な方法ではありません。  
  
 次のプロシージャでは、再帰を使用して元の引数の階乗を計算します。  
  
 [!code-vb[VbVbcnProcedures#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#51)]  
  
## <a name="considerations-with-recursive-procedures"></a>再帰プロシージャに関する考慮事項

 **制限条件**。 再帰を終了できる条件を少なくとも 1 つはテストするように、再帰プロシージャを設計する必要があります。また、妥当な回数の再帰呼び出しでそのような条件が満たされない場合の処理も必要となります。 必ず満たすことができる条件が少なくとも 1 つはないと、プロシージャが無限ループで実行されるリスクが高くなります。

 **メモリ使用状況**。 アプリケーションがローカル変数に使用できる領域は限られています。 プロシージャが自身を呼び出すたびに、ローカル変数のコピーが追加され、その領域が使用されます。 このプロセスが無期限に続行されると、最終的に <xref:System.StackOverflowException> エラーが発生します。

 **効率**。 ほとんどの場合、再帰の代わりにループを使用できます。 ループには、引数を渡し、追加のストレージを初期化して、値を返すというオーバーヘッドはありません。 再帰呼び出しがない場合、パフォーマンスが大幅に向上します。

 **相互再帰**。 2 つのプロシージャが相互に呼び出し合うと、パフォーマンスが大幅に低下したり、無限ループが発生したりする可能性があります。 このような設計では、単一の再帰プロシージャと同じ問題が発生しますが、検出とデバッグがより困難になることがあります。

 **かっこを使用した呼び出し**。 `Function` プロシージャが自身を再帰的に呼び出すときには、引数リストがない場合でも、プロシージャ名の後にかっこを使用する必要があります。 そうしないと、関数名が関数の戻り値を表していると見なされます。

 **テスト**。 再帰プロシージャを作成した場合は、慎重にテストして、何らかの制限条件を常に満たしていることを確認する必要があります。 また、再帰呼び出しが多すぎるためにメモリ不足にならないようにする必要があります。

## <a name="see-also"></a>関連項目

- <xref:System.StackOverflowException>
- [手順](index.md)
- [Sub プロシージャ](sub-procedures.md)
- [Function プロシージャ](function-procedures.md)
- [Property プロシージャ](property-procedures.md)
- [演算子プロシージャ](operator-procedures.md)
- [プロシージャのパラメーターと引数](procedure-parameters-and-arguments.md)
- [プロシージャのオーバーロード](procedure-overloading.md)
- [プロシージャのトラブルシューティング](troubleshooting-procedures.md)
- [ループ構造](../control-flow/loop-structures.md)
