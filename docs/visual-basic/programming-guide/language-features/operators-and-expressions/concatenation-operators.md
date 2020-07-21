---
title: 連結演算子
ms.date: 07/20/2015
helpviewer_keywords:
- '& operator [Visual Basic], concatenation'
- concatenation operators [Visual Basic]
- operators [Visual Basic], concatenation
- Visual Basic code, operators
- + operator [Visual Basic], concatenation
- concatenation operators [Visual Basic]
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
ms.openlocfilehash: c123438a86a2c3293a99770107d970535fcdbdf8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388791"
---
# <a name="concatenation-operators-in-visual-basic"></a>Visual Basic の連結演算子

連結演算子は、複数の文字列を結合して 1 つの文字列にします。 連結演算子には、`+` と `&` の 2 つがあります。 どちらの演算子も、次の例に示すように基本的な連結演算を行います。

```vb
Dim x As String = "Mic" & "ro" & "soft"
Dim y As String = "Mic" + "ro" + "soft"
' The preceding statements set both x and y to "Microsoft".
```

これらの演算子は、次のように `String` 型の変数を連結することもできます。

[!code-vb[VbVbalrOperators#76](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#76)]

## <a name="differences-between-the-two-concatenation-operators"></a>2 つの連結演算子の相違点

[+ 演算子](../../../language-reference/operators/addition-operator.md)の基本的な目的は、2 つの数値を加算することです。 ただし、数値オペランドを文字列オペランドに連結することもできます。 `+` 演算子は、一連の複雑な規則に従って、加算、連結、コンパイル エラーのシグナルの送信、ランタイム <xref:System.InvalidCastException> 例外のスローのどれを行うかを決定します。

[& 演算子](../../../language-reference/operators/concatenation-operator.md)は、`String` オペランドに対してのみ定義され、`Option Strict` の設定に関係なく、常にそのオペランドを `String` に拡大変換します。 文字列の連結には `&` 演算子を使用することをお勧めします。この演算子は文字列専用として定義されているため、意図しない変換が発生する可能性を減らすことができます。

## <a name="performance-string-and-stringbuilder"></a>パフォーマンス: String と StringBuilder

連結、削除、置換などの文字列操作を何度も行う場合は、<xref:System.Text.StringBuilder> 名前空間の <xref:System.Text> クラスを使用するとパフォーマンスが向上します。 <xref:System.Text.StringBuilder> オブジェクトを作成して初期化するには追加の命令が必要であり、最終的な値を `String` に変換するにはまた別の命令が必要になりますが、<xref:System.Text.StringBuilder> は高速に実行できるため、この時間を埋め合わせることができます。

## <a name="see-also"></a>関連項目

- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
- [Visual Basic における文字列操作メソッドの種類](../strings/types-of-string-manipulation-methods.md)
- [Visual Basic における算術演算子](arithmetic-operators.md)
- [Visual Basic における比較演算子](comparison-operators.md)
- [Visual Basic の論理演算子とビット処理演算子](logical-and-bitwise-operators.md)
