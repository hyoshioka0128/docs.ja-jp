---
title: Visual Basic の演算子で実行される一般的な演算
ms.date: 07/20/2015
helpviewer_keywords:
- operators [Visual Basic], logical
- operators [Visual Basic], string concatenation
- operators [Visual Basic], bitwise
- operators [Visual Basic], bit-shift
- operators [Visual Basic], arithmetic
- operators [Visual Basic], string comparison
- operators [Visual Basic], concatenation
- Visual Basic code, operators
- operators [Visual Basic], comparison
- operators [Visual Basic], short-circuiting logical
ms.assetid: d181afe5-fafa-460f-a13b-81203f6f4587
ms.openlocfilehash: 62ced7f2048ae41c7ea4c9d62c0ff0a903c37856
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388921"
---
# <a name="common-tasks-performed-with-visual-basic-operators"></a>Visual Basic の演算子で実行される一般的な演算
演算子によって、"*オペランド*" と呼ばれる 1 つ以上の式を含む多くの一般的なタスクが実行されます。  
  
## <a name="arithmetic-and-bit-shift-tasks"></a>算術とビットシフト タスク  
 次の表は、使用できる算術演算とビットシフト演算をまとめたものです。  
  
|終了|解決方法については、|  
|---|---|  
|ある数値をもう 1 つの数値に加算します|[+ 演算子](../../../language-reference/operators/addition-operator.md)|  
|ある数値からもう 1 つの数値を減算します|[- 演算子 (Visual Basic)](../../../language-reference/operators/subtraction-operator.md)|  
|ある数値の符号を反転します|[- 演算子 (Visual Basic)](../../../language-reference/operators/subtraction-operator.md)|  
|ある数値にもう 1 つの数値を乗算します|[* 演算子](../../../language-reference/operators/multiplication-operator.md)|  
|ある数値をもう 1 つの数値に除算します|[/ 演算子 (Visual Basic)](../../../language-reference/operators/floating-point-division-operator.md)|  
|ある数値をもう 1 つの数値で除算した商を求めます (剰余なし)|[\ 演算子 (Visual Basic)](../../../language-reference/operators/integer-division-operator.md)|  
|ある数値をもう 1 つの数値で除算した剰余を求めます (商なし)|[Mod 演算子](../../../language-reference/operators/mod-operator.md)|  
|ある数値をもう 1 つの数値のべき乗にします|[^ 演算子](../../../language-reference/operators/exponentiation-operator.md)|  
|数値のビット パターンを左にシフトします|[<\< 演算子](../../../language-reference/operators/left-shift-operator.md)|  
|数値のビット パターンを右にシフトします|[>> 演算子](../../../language-reference/operators/right-shift-operator.md)|  
  
## <a name="comparison-tasks"></a>比較タスク  
 次の表は、使用できる比較演算をまとめたものです。  
  
|終了|解決方法については、|  
|---|---|  
|2 つの値が等しいかどうかを判断します|`=` 演算子 ([Visual Basic の比較演算子](comparison-operators.md))|  
|2 つの値が等しくないかどうかを判断します|`<>` 演算子 ([Visual Basic の比較演算子](comparison-operators.md))|  
|ある値がもう 1 つの値より小さいかどうかを判断します|`<` 演算子 ([Visual Basic の比較演算子](comparison-operators.md))|  
|ある値がもう 1 つの値より大きいかどうかを判断します|`>` 演算子 ([Visual Basic の比較演算子](comparison-operators.md))|  
|ある値がもう 1 つの値以下かどうかを判断します|`<=` 演算子 ([Visual Basic の比較演算子](comparison-operators.md))|  
|ある値がもう 1 つの値以上かどうかを判断します|`>=` 演算子 ([Visual Basic の比較演算子](comparison-operators.md))|  
|2 つのオブジェクト変数が同じオブジェクト インスタンスを参照しているかどうかを判断します|[Is 演算子](../../../language-reference/operators/is-operator.md)|  
|2 つのオブジェクト変数が異なるオブジェクト インスタンスを参照しているかどうかを判断します|[IsNot 演算子](../../../language-reference/operators/isnot-operator.md)|  
|オブジェクトが特定の型であるかどうかを判断します|[TypeOf 演算子](../../../language-reference/operators/typeof-operator.md)|  
  
## <a name="concatenation-tasks"></a>連結タスク  
 次の表は、使用できる連結演算をまとめたものです。  
  
|終了|解決方法については、|  
|---|---|  
|複数の文字列を 1 つの文字列に結合します|`&` 演算子 ([Visual Basic の連結演算子](concatenation-operators.md))|  
|数値と文字列値を結合します|`+` 演算子 ([Visual Basic の連結演算子](concatenation-operators.md))|  
  
## <a name="logical-and-bitwise-tasks"></a>論理タスクとビットごとのタスク  
 次の表は、使用できる論理演算とビットごとの演算をまとめたものです。  
  
|終了|解決方法については、|  
|---|---|  
|ブール値に対して論理否定を実行します|[Not 演算子](../../../language-reference/operators/not-operator.md)|  
|2 つのブール値に対して論理積を実行します|[And 演算子](../../../language-reference/operators/and-operator.md)|  
|2 つのブール値に対して包括的論理和演算を実行します|[Or 演算子](../../../language-reference/operators/or-operator.md)|  
|2 つのブール値に対して排他的論理和演算を実行します|[Xor 演算子](../../../language-reference/operators/xor-operator.md)|  
|2 つのブール値に対して短絡論理積を実行します|[AndAlso 演算子](../../../language-reference/operators/andalso-operator.md)|  
|2 つのブール値に対して短絡包括的論理和演算を実行します|[OrElse 演算子](../../../language-reference/operators/orelse-operator.md)|  
|2 つの整数値に対してビット単位の論理積を実行します|[And 演算子](../../../language-reference/operators/and-operator.md)|  
|2 つの整数値に対してビット単位の包括的論理和演算を実行します|[Or 演算子](../../../language-reference/operators/or-operator.md)|  
|2 つの整数値に対してビット単位の排他的論理和演算を実行します|[Xor 演算子](../../../language-reference/operators/xor-operator.md)|  
|整数値に対してビット単位の論理否定を実行します|[Not 演算子](../../../language-reference/operators/not-operator.md)|  
  
## <a name="see-also"></a>関連項目

- [演算子および式](index.md)
- [機能別の演算子一覧](../../../language-reference/operators/operators-listed-by-functionality.md)
