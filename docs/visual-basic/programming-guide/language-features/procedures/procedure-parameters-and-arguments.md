---
title: プロシージャのパラメーターと引数
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], argument lists
- values [Visual Basic], passing to procedures
- arguments [Visual Basic], passing
- procedures [Visual Basic], parameters
- Visual Basic code, argument lists
- Visual Basic code, procedures
- parameters [Visual Basic], Visual Basic procedures
- parameters [Visual Basic], lists
- arguments [Visual Basic], Visual Basic procedures
- arguments [Visual Basic], procedures
- parameter lists [Visual Basic]
- Visual Basic code, parameter lists
- argument lists [Visual Basic]
- procedures [Visual Basic], parameter lists
ms.assetid: ff275aff-aa13-40df-bd4c-63486db8c1e9
ms.openlocfilehash: 178206ca2ee103bbdb5a4ac03bca0df903c8c5d8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406717"
---
# <a name="procedure-parameters-and-arguments-visual-basic"></a>プロシージャのパラメーターと引数 (Visual Basic)
ほとんどの場合、プロシージャには呼び出された状況に関する情報が必要です。 反復的なタスクや共有タスクを実行するプロシージャでは、呼び出しごとに異なる情報を使用します。 この情報は、呼び出し時にプロシージャに渡す変数、定数、式で構成されます。  
  
 "*パラメーター*" は、プロシージャを呼び出すときに指定する必要がある値を表します。 プロシージャの宣言でパラメーターを定義します。  
  
 パラメーターなし、1 つのパラメーター、または複数のパラメーターでプロシージャを定義できます。 プロシージャ定義の、パラメーターを指定する部分は、"*パラメーター リスト*" と呼ばれます。  
  
 "*引数*" は、プロシージャを呼び出すときにプロシージャ パラメーターに指定する値を表します。 呼び出し元のコードは、プロシージャを呼び出すときに引数を指定します。 プロシージャ呼び出しの、引数を指定する部分は、"*引数リスト*" と呼ばれます。  
  
 次の図は、2 つの異なる場所から `safeSquareRoot` プロシージャを呼び出すコードを示しています。 最初の呼び出しでは、変数 `x` の値 (4.0) を `number` パラメーターに渡し、`root` の戻り値 (2.0) が変数 `y` に割り当てられます。 2 番目の呼び出しでは、リテラル値 9.0 を `number` に渡し、戻り値 (3.0) を変数 `z` に割り当てます。  
  
 ![パラメーターへの引数の引渡しを示す図](./media/procedure-parameters-and-arguments/pass-argument-parameter.gif)  
  
 詳細については、「[Differences Between Parameters and Arguments (パラメーターと引数の違い)](./differences-between-parameters-and-arguments.md)」をご覧ください。  
  
## <a name="parameter-data-type"></a>パラメーターのデータ型  
 パラメーターのデータ型を定義するには、宣言で `As` 句を使用します。 たとえば、次の関数は文字列と整数を受け入れます。  
  
 [!code-vb[VbVbcnProcedures#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#32)]  
  
 型チェック スイッチ ([Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)) が `Off,` の場合、`As` 句は省略可能です。ただし、いずれか 1 つのパラメーターで使用する場合は、すべてのパラメーターで使用する必要があります。 型チェックが `On` の場合は、すべてのプロシージャ パラメーターで `As` 句が必須となります。  
  
 呼び出し元のコードが、対応するパラメーターのデータ型とは異なるデータ型の引数 (`String` パラメーターに対する `Byte` など) を指定することを要求している場合、次のいずれかを実行する必要があります。  
  
- パラメーターのデータ型に拡大変換するデータ型の引数のみを指定する。  
  
- `Option Strict Off` を設定して、暗黙的な縮小変換を許可する。または、  
  
- 変換キーワードを使用して、データ型を明示的に変換する。  
  
### <a name="type-parameters"></a>型パラメーター  
 "*ジェネリック プロシージャ*" では、通常のパラメーターに加え、1 つ以上の "*型パラメーター*" も定義します。 ジェネリック プロシージャを使用すると、呼び出し元のコードは、プロシージャを呼び出すたびに異なるデータ型を渡すことができるため、個々の呼び出しの要件に合わせてデータ型を調整できます。 「 [Generic Procedures in Visual Basic](../data-types/generic-procedures.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [Function プロシージャ](./function-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [演算子プロシージャ](./operator-procedures.md)
- [方法: プロシージャのパラメーターを定義する](./how-to-define-a-parameter-for-a-procedure.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [Visual Basic における型変換](../data-types/type-conversions.md)
