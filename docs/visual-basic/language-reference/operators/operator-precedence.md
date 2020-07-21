---
title: 演算子の優先順位
ms.date: 07/20/2015
helpviewer_keywords:
- arithmetic operators [Visual Basic], precedence
- operator precedence
- logical operators [Visual Basic], precedence
- operators [Visual Basic], associativity
- operators [Visual Basic], resolution
- associativity of operators [Visual Basic]
- operators [Visual Basic], precedence
- precedence [Visual Basic], of operators
- comparison operators [Visual Basic], precedence
- math operators [Visual Basic]
- order of precedence
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
ms.openlocfilehash: eef6314f5fc1f5a7fffa7997559f697130f6f755
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401447"
---
# <a name="operator-precedence-in-visual-basic"></a>Visual Basic における演算子の優先順位
式で複数の演算が行われると、各部分は "*演算子の優先順位*" と呼ばれる事前に定義された順序で評価および解決されます。

## <a name="precedence-rules"></a>優先順位の規則
 式に複数のカテゴリの演算子が含まれている場合は、次の規則に従って評価されます。

- 算術演算子と連結演算子には、次のセクションで説明する優先順位があり、これらはすべて比較演算子、論理演算子、ビット演算子よりも優先順位が高くなります。

- すべての比較演算子は同じ優先順位を持ち、論理演算子とビット演算子より優先順位が高くなりますが、算術演算子と連結演算子より優先順位が低くなります。

- 論理演算子とビット演算子には、次のセクションで説明する優先順位があり、これらはすべて算術演算子、連結演算子、比較演算子よりも優先順位が低くなります。

- 優先順位が同じ演算子は、式に出現する順序で左から右に評価されます。

## <a name="precedence-order"></a>優先順位
 演算子は次の優先順位で評価されます。

### <a name="await-operator"></a>Await 演算子
 Await

### <a name="arithmetic-and-concatenation-operators"></a>算術演算子と連結演算子
 累乗 (`^`)

 単項恒等と否定 (`+`、`–`)

 乗算および浮動小数点除算 (`*`、`/`)

 整数の除算 (`\`)

 モジュラー演算 (`Mod`)

 加算と減算 (`+`、`–`)

 文字列連結 (`&`)

 算術ビット シフト (`<<`、`>>`)

### <a name="comparison-operators"></a>比較演算子
 すべての比較演算子 (`=`、`<>`、`<`、`<=`、`>`、`>=`、`Is`、`IsNot`、`Like`、`TypeOf`...`Is`)

### <a name="logical-and-bitwise-operators"></a>論理演算子とビット処理演算子
 否定 (`Not`)

 接続詞 (`And`、`AndAlso`)

 包含的論理和 (`Or`、`OrElse`)

 排他的論理和 (`Xor`)

### <a name="comments"></a>コメント
 `=` 演算子は単に等値比較演算子であり、代入演算子ではありません。

 文字列連結演算子 (`&`) は算術演算子ではありませんが、優先順位においては算術演算子と同じグループに分類されます。

 `Is` と `IsNot` の演算子は、オブジェクト参照比較演算子です。 これらは 2つのオブジェクトの値を比較しません。2 つのオブジェクト変数が同じオブジェクト インスタンスを参照するかどうかを確認するだけです。

## <a name="associativity"></a>結合規則
 同じ優先順位の演算子が乗算や除算などの式に一緒に現れる場合、コンパイラは各演算の出現時にそれを左から右に評価します。 次の例を使って説明します。

```vb
Dim n1 As Integer = 96 / 8 / 4
Dim n2 As Integer = (96 / 8) / 4
Dim n3 As Integer = 96 / (8 / 4)
```

 最初の式では、除算 96/8 (結果は 12) が評価され、次に除算 12/4 (結果は 3) が評価されます。 コンパイラでは `n1` の演算が左から右に評価されるため、その順序が `n2` に明示的に指定されている場合、評価は同じになります。 `n1` と `n2` の両方の結果が 3 になります。 これに対して、`n3` の結果は 48 になります。これは、かっこによりコンパイラで 8/4 が最初に評価されるためです。

 この動作のため、演算子は Visual Basic 内で "*結合規則が左から右*" であると言われます。

## <a name="overriding-precedence-and-associativity"></a>優先順位と結合規則のオーバーライド
 かっこを使用して、式のいくつかの部分を他の部分より前に強制的に評価できます。 これにより、優先順位と左から右の結合規則の両方をオーバーライドできます。 Visual Basic では常に、かっこで囲まれた演算がその外側にある演算より前に実行されます。 ただし、かっこで内では、通常の優先順位と結合規則が維持されます (かっこ内でかっこを使用する場合は除く)。 次の例を使って説明します。

```vb
Dim a, b, c, d, e, f, g As Double
a = 8.0
b = 3.0
c = 4.0
d = 2.0
e = 1.0
f = a - b + c / d * e
' The preceding line sets f to 7.0. Because of natural operator
' precedence and associativity, it is exactly equivalent to the
' following line.
f = (a - b) + ((c / d) * e)
' The following line overrides the natural operator precedence
' and left associativity.
g = (a - (b + c)) / (d * e)
' The preceding line sets g to 0.5.
```

## <a name="see-also"></a>関連項目

- [= 演算子](assignment-operator.md)
- [Is 演算子](is-operator.md)
- [IsNot 演算子](isnot-operator.md)
- [Like 演算子](like-operator.md)
- [TypeOf 演算子](typeof-operator.md)
- [Await 演算子](await-operator.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
