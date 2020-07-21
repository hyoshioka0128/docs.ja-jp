---
title: 演算子の効率のよい組み合わせ
ms.date: 07/20/2015
helpviewer_keywords:
- expressions [Visual Basic], parentheses
- operators [Visual Basic], associativity
- expressions [Visual Basic], operators
- operators [Visual Basic], precedence
- Visual Basic code, operators
- Visual Basic code, expressions
- operators [Visual Basic], complex expressions
- expressions [Visual Basic], complex
- parentheses [Visual Basic], complex expressions
- numeric expressions
ms.assetid: bd22340e-b5be-458b-8772-3916c02309a4
ms.openlocfilehash: 3088072646278dac13e4d483cb4f99297eaad9ca
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403473"
---
# <a name="efficient-combination-of-operators-visual-basic"></a>演算子の効率のよい組み合わせ (Visual Basic)
複合式にはさまざまな演算子を含めることができます。 次の例を使って説明します。  
  
 `x = (45 * (y + z)) ^ (2 / 85) * 5 + z`  
  
 前の例のいずれかのような複雑な式を作成するには、演算子の優先順位のルールを十分に理解している必要があります。 詳細については、「[Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)」を参照してください。  
  
## <a name="parenthetical-expressions"></a>かっこで囲まれた式  
 多くの場合、演算子の優先順位によって決定される順序とは異なる順序で操作を進める必要があります。 例を次に示します。  
  
 `x = z * y + 4`  
  
 前の例では、`z` を `y` で乗算し、その結果を `4` に加算しています。 ただし、結果を `z` で乗算する前に `y` と `4` を加算する場合は、かっこを使用して通常の演算子の優先順位をオーバーライドできます。 式をかっこで囲むことで、演算子の優先順位に関係なく、強制的にその式が最初に評価されます。 前の例で強制的に最初に加算を行うには、次の例のように記述し直します。  
  
 `x = z * (y + 4)`  
  
 前の例では、`y` と `4` を加算し、その合計を `z` で乗算しています。  
  
### <a name="nested-parenthetical-expressions"></a>入れ子になったかっこで囲まれた式  
 式を複数のレベルのかっこで入れ子にして、優先順位をさらにオーバーライドすることができます。 かっこ内で最も深く入れ子にされている式が最初に評価され、次に最も深く入れ子にされている式、次に最も深く入れ子にされていない式、最後にかっこの外側の式が評価されます。 次の例を使って説明します。  
  
 `x = (z * 4) ^ (y * (z + 2))`  
  
 前の例では、最初に `z + 2` が評価され、その後、かっこで囲まれたその他の式が評価されます。 通常、加算または乗算よりも高い優先順位を持つ指数演算は、この例では最後に評価されます。これは、他の式がかっこで囲まれているためです。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における算術演算子](arithmetic-operators.md)
- [Visual Basic における比較演算子](comparison-operators.md)
- [Visual Basic の論理演算子とビット処理演算子](logical-and-bitwise-operators.md)
- [論理/ビット演算子 (Visual Basic)](../../../language-reference/operators/logical-bitwise-operators.md)
- [ブール式](boolean-expressions.md)
- [値の比較](value-comparisons.md)
- [方法: 数値を計算する](how-to-calculate-numeric-values.md)
- [Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)
