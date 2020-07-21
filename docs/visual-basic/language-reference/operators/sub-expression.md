---
title: 部分式
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [Visual Basic], sub expression
- Sub Expression [Visual Basic]
- subroutines [Visual Basic], sub expressions
ms.assetid: 36b6bfd1-6539-4d8f-a5eb-6541a745ffde
ms.openlocfilehash: f862730220d0595faecaa915b1eaad2a3cdc0053
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406316"
---
# <a name="sub-expression-visual-basic"></a>部分式 (Visual Basic)
サブルーチン ラムダ式を定義するパラメーターとコードを宣言します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Sub ( [ parameterlist ] ) statement  
- or -  
Sub ( [ parameterlist ] )  
  [ statements ]  
End Sub  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`parameterlist`|任意。 プロシージャのパラメーターを表すローカル変数名のリスト。 リストが空の場合でも、かっこが存在する必要があります。 詳細については、「 [Parameter List](../statements/parameter-list.md)」を参照してください。|  
|`statement`|必須です。 1 つのステートメント。|  
|`statements`|必須です。 ステートメントの一覧。|  
  
## <a name="remarks"></a>Remarks  
 *ラムダ式*は、1 つ以上のステートメントを実行する、名前のないサブルーチンです。 ラムダ式は、デリゲート型を使用できる場所であればどこでも使用できます。ただし、`RemoveHandler` の引数として使用することはできません。 デリゲートの詳細と、デリゲートでのラムダ式の使用の詳細については、「[Delegate ステートメント](../statements/delegate-statement.md)」と「[厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)」をご覧ください。  
  
## <a name="lambda-expression-syntax"></a>ラムダ式の構文  
 ラムダ式の構文は、標準のサブルーチンの構文に似ています。 相違点は、次のとおりです。  
  
- ラムダ式には名前がありません。  
  
- ラムダ式には、`Overloads` や `Overrides` などの修飾子を含めることはできません。  
  
- 単一行のラムダ式の本体は、式ではなく、ステートメントでなければなりません。 本体は、サブ プロシージャの呼び出しで構成できますが、関数プロシージャの呼び出しでは構成できません。  
  
- ラムダ式では、すべてのパラメーターに対してデータ型を指定する必要があります。または、すべてのパラメーターを推論できる必要があります。  
  
- ラムダ式では、省略可能なパラメーターと `ParamArray` パラメーターは使用できません。  
  
- ラムダ式では、ジェネリック パラメーターは使用できません。  
  
## <a name="example"></a>例  
 次の例は、コンソールに値を書き込むラムダ式です。 この例は、サブルーチンの単一行および複数行のラムダ式の構文を示しています。 その他の例については、「[ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)」を参照してください。  
  
 [!code-vb[VbVbalrLambdas#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>関連項目

- [Sub ステートメント](../statements/sub-statement.md)
- [ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
- [厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
