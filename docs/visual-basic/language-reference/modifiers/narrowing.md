---
title: Narrowing
ms.date: 07/20/2015
f1_keywords:
- vb.narrowing
helpviewer_keywords:
- conversions [Visual Basic], type
- type conversion [Visual Basic]
- conversions [Visual Basic], data type
- Narrowing keyword [Visual Basic]
- data type conversion [Visual Basic]
ms.assetid: a207ee91-aca4-4771-b4e2-713f029bf2bb
ms.openlocfilehash: f7724053e3732c909523e4e2d3b65bb1918c29d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84362360"
---
# <a name="narrowing-visual-basic"></a>Narrowing (Visual Basic)
変換演算子 (`CType`) で、クラスまたは構造体を、元のクラスまたは構造体の一部の使用可能な値を保持できない可能性がある型に変換することを示します。  
  
## <a name="converting-with-the-narrowing-keyword"></a>Narrowing キーワードを使用した変換  
 変換プロシージャでは、`Narrowing` に加えて `Public Shared` を指定する必要があります。  
  
 縮小変換は実行時に必ず成功するとは限らず、失敗したり、データの損失が発生したりする可能性があります。 例として、`Long` から `Integer`、`String` から `Date`、および基本型から派生型があります。 基本型には派生型のすべてのメンバーが含まれていない場合があり、派生型のインスタンスではないため、この最後の変換は縮小変換になります。  
  
 `Option Strict` が `On` の場合、使用しているコードではすべての縮小変換に `CType` を使用する必要があります。  
  
 `Narrowing` キーワードは次のコンテキストで使用できます。  
  
 [Operator ステートメント](../statements/operator-statement.md)  
  
## <a name="see-also"></a>関連項目

- [Operator ステートメント](../statements/operator-statement.md)
- [Widening](widening.md)
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [方法: 演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [CType 関数](../functions/ctype-function.md)
- [Option Strict ステートメント](../statements/option-strict-statement.md)
