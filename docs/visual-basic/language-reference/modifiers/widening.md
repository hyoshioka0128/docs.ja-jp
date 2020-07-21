---
title: Widening
ms.date: 07/20/2015
f1_keywords:
- vb.widening
helpviewer_keywords:
- conversions [Visual Basic], type
- type conversion [Visual Basic]
- conversions [Visual Basic], data type
- Widening keyword [Visual Basic]
- data type conversion [Visual Basic]
ms.assetid: 646ae263-94d3-40a2-b0cc-64f619292f56
ms.openlocfilehash: 69040bf48b44a54f7a231738b88db1cbc716ebb3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359904"
---
# <a name="widening-visual-basic"></a>Widening (Visual Basic)
変換演算子 (`CType`) が、クラスまたは構造体を、元のクラスまたは構造体のすべての使用可能な値を保持できる型に変換することを示します。  
  
## <a name="converting-with-the-widening-keyword"></a>Widening キーワードを使用した変換  
 変換プロシージャでは、`Widening` に加えて `Public Shared` を指定する必要があります。  
  
 拡大変換は実行時に必ず成功し、データの損失が発生することはありません。 例として、`Single` から `Double`、`Char` から `String`、および派生型からその基本型があります。 この最後の変換は拡大変換です。これは、派生型に基本型のすべてのメンバーが含まれており、基本型のインスタンスであるためです。  
  
 `Option Strict` が `On` の場合でも、使用するコードが拡大変換に `CType` を使用する必要はありません。  
  
 `Widening` キーワードは次のコンテキストで使用できます。  
  
 [Operator ステートメント](../statements/operator-statement.md)  
  
 拡大変換と縮小変換の演算子の定義の例については、「[方法: 変換演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Operator ステートメント](../statements/operator-statement.md)
- [Narrowing](narrowing.md)
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [方法: 演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [CType 関数](../functions/ctype-function.md)
- [Option Strict ステートメント](../statements/option-strict-statement.md)
- [方法: 変換演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
