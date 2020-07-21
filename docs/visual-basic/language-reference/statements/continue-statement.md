---
title: Continue ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.continue
helpviewer_keywords:
- Continue statement [Visual Basic]
- loops, transferring to next iteration
ms.assetid: 3ad00103-358b-4af3-a3a8-1b9ea0e995d3
ms.openlocfilehash: fd604b281a590073a5e76398788d7648cadd145c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84382095"
---
# <a name="continue-statement-visual-basic"></a>Continue ステートメント (Visual Basic)
ループの次の反復に直ちに制御を移します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Continue { Do | For | While }  
```  
  
## <a name="remarks"></a>Remarks  
 `Do`、`For`、または `While` ループ内から、そのループの次の反復に移すことができます。 制御はすぐにループ条件テストに渡されます。これは、`For` または `While` ステートメントに移ったり、`Until` または `While` 句が含まれている `Do` または `Loop` ステートメントに移ったりするのと同じです。  
  
 `Continue` は、移動を許可するループ内の任意の場所で使用できます。 制御の移動を許可するルールは、[GoTo ステートメント](goto-statement.md)を使用する場合と同じです。  
  
 たとえば、ループが `Try` ブロック、`Catch` ブロック、または `Finally` ブロック内に完全に含まれている場合は、`Continue` を使用してループから移動できます。 一方、`Try`...`End Try` 構造体がループ内に含まれている場合は、`Continue` を使用して `Finally` ブロックから制御を移すことはできません。これを使用して `Try` または `Catch` ブロックから移すことができるのは、`Try`...`End Try` 構造体から完全に移す場合のみです。  
  
 同じ種類のループが入れ子になっている場合 (別の `Do` ループ内の `Do` ループなど)、`Continue Do` ステートメントは、それが含まれている最も内側の `Do` ループの次の反復にスキップします。 `Continue` を使用して、同じ種類の含まれているループの次の反復にスキップすることはできません。  
  
 さまざまな種類のループが入れ子になっている場合 (`For` ループ内の `Do` ループなど)、`Continue Do` または `Continue For` のいずれかを使用して、いずれかのループの次の反復にスキップできます。  
  
## <a name="example"></a>例  
 次のコード例では、除数が 0 の場合に、`Continue While` ステートメントを使用して配列の次の列にスキップします。 `Continue While` は `For` ループ内にあります。 これにより `While col < lastcol` ステートメントに移動します。これは、`For` ループが含まれている最も内側の `While` ループの次の反復です。  
  
 [!code-vb[VbVbalrStatements#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#14)]  
  
## <a name="see-also"></a>関連項目

- [Do...Loop ステートメント](do-loop-statement.md)
- [For...Next ステートメント](for-next-statement.md)
- [While...End While ステートメント](while-end-while-statement.md)
- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
