---
title: '方法: 値を返すプロシージャを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- procedure calls [Visual Basic], returning values
- Visual Basic code, procedures
- procedures [Visual Basic], calling
- procedures [Visual Basic], returning a value
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
ms.openlocfilehash: a110cf9f3b42c7244d8d5bf7b49d5e6dac8c2e21
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388765"
---
# <a name="how-to-call-a-procedure-that-returns-a-value-visual-basic"></a>方法: 値を返すプロシージャを呼び出す (Visual Basic)
`Function` プロシージャからは、呼び出し元のコードに値が返されます。 それを呼び出すには、その名前と引数を代入ステートメントの右辺に、または式に含めます。  
  
### <a name="to-call-a-function-procedure-within-an-expression"></a>式内で Function プロシージャを呼び出すには  
  
1. `Function` プロシージャ名は、変数を使用する場合と同じ方法で使用します。 式内の変数または定数を使用できる場所であればどこでも、`Function` プロシージャ呼び出しを使用できます。  
  
2. プロシージャ名の後にかっこを使用して引数リストを囲みます。 引数がない場合は、必要に応じてかっこを省略できます。 ただし、かっこを使用すると、コードが読みやすくなります。  
  
3. 引数リストの引数をコンマで区切ってかっこ内に配置します。 引数の指定は必ず、`Function` プロシージャで定義されている対応するパラメーターと同じ順序で行ってください。  
  
     または、1 つまたは複数の引数を名前で渡すこともできます。 詳細については、「[位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)」を参照してください。  
  
4. プロシージャから返される値は、変数または定数の値と同じように、式に含められます。  
  
### <a name="to-call-a-function-procedure-in-an-assignment-statement"></a>代入ステートメントで Function プロシージャを呼び出すには  
  
1. 代入ステートメント内で等号 (`=`) の後に `Function` プロシージャ名を使用します。  
  
2. プロシージャ名の後にかっこを使用して引数リストを囲みます。 引数がない場合は、必要に応じてかっこを省略できます。 ただし、かっこを使用すると、コードが読みやすくなります。  
  
3. 引数リストの引数をコンマで区切ってかっこ内に配置します。 引数を名前で渡さない場合、それらは必ず、`Function` プロシージャで定義されている対応するパラメーターと同じ順序で指定してください。  
  
4. プロシージャから返された値は、代入ステートメントの左側にある変数またはプロパティに格納されます。  
  
## <a name="example"></a>例  
 次の例では、Visual Basic <xref:Microsoft.VisualBasic.Interaction.Environ%2A> を呼び出して、オペレーティング システムの環境変数の値を取得します。 最初の行では式内で `Environ` が呼び出され、2 番目の行では代入ステートメントでそれが呼び出されます。 `Environ` では、その唯一の引数として変数名を取ります。 これにより、呼び出し元のコードに変数の値が返されます。  
  
 [!code-vb[VbVbcnProcedures#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#7)]  
  
## <a name="see-also"></a>関連項目

- [Function プロシージャ](./function-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Function ステートメント](../../../language-reference/statements/function-statement.md)
- [方法: 値を返すプロシージャを作成する](./how-to-create-a-procedure-that-returns-a-value.md)
- [方法: プロシージャから値を返す](./how-to-return-a-value-from-a-procedure.md)
- [方法: 値を返さないプロシージャを呼び出す](./how-to-call-a-procedure-that-does-not-return-a-value.md)
