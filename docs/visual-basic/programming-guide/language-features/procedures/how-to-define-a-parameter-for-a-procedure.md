---
title: '方法: プロシージャにパラメーターを定義する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedure parameters [Visual Basic], defining data types for
- procedures [Visual Basic], parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters [Visual Basic], defining
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
ms.openlocfilehash: e703346113348556b8a3ea41a7934a55a8008522
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388077"
---
# <a name="how-to-define-a-parameter-for-a-procedure-visual-basic"></a>方法: プロシージャにパラメーターを定義する (Visual Basic)
"*パラメーター*" では、その呼び出し時に呼び出し元コードでプロシージャに値を渡すことができます。 プロシージャの各パラメーターは、変数を宣言する場合と同じ方法で、その名前とデータ型を指定して宣言します。 引渡し方法と、パラメーターが省略可能かどうかを指定することもできます。  
  
 詳細については、「[プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)」を参照してください。  
  
### <a name="to-define-a-procedure-parameter"></a>プロシージャのパラメーターを定義するには  
  
1. プロシージャの宣言では、プロシージャのパラメーター リストにパラメーター名を追加し、他のパラメーターとコンマで区切ります。  
  
2. パラメーターのデータ型を決定します。  
  
3. パラメーター名の後に `As` 句を付けて、データ型を指定します。  
  
4. パラメーターに必要な引渡し方法を決定します。 プロシージャで呼び出し元コードの値を変更できるようにする必要がある場合を除き、通常は値でパラメーターを渡します。  
  
5. パラメーター名の前に [ByVal](../../../language-reference/modifiers/byval.md) または [ByRef](../../../language-reference/modifiers/byref.md) を付けて、引渡し方法を指定します。 詳細については、「[引数の値渡しと参照渡しの違い](./differences-between-passing-an-argument-by-value-and-by-reference.md)」を参照してください。  
  
6. パラメーターが省略可能な場合は、引渡し方法の前に [Optional](../../../language-reference/modifiers/optional.md) を付け、パラメーターのデータ型の後に等号 (`=`) と既定値を付けます。  
  
     次の例では、3 つのパラメーターがある `Sub` プロシージャを定義します。 最初の 2 つは必須で、3 つ目は省略可能です。 パラメーターの宣言は、パラメーター リスト内でコンマで区切られます。  
  
     [!code-vb[VbVbcnProcedures#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#33)]  
  
     最初のパラメーターでは `customer` オブジェクトを受け入れ、`updateCustomer` では `c` に渡された変数を直接更新することができます。これは、引数が [ByRef](../../../language-reference/modifiers/byref.md) で渡されるためです。 このプロシージャでは、最後の 2 つの引数の値を変更することはできません。これは、それらが [ByVal](../../../language-reference/modifiers/byval.md) で渡されるためです。  
  
     呼び出し元コードで `level` パラメーターの値が指定されていない場合は、Visual Basic で既定値の 0 に設定されます。  
  
     型チェック スイッチ ([Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)) が `Off` の場合は、パラメーターを定義するときに `As` 句を省略できます。 しかし、いずれかのパラメーターで `As` 句を使用する場合は、それらすべてで使用する必要があります。 型チェック スイッチが `On` の場合は、すべてのパラメーター定義に対して `As` 句が必須となります。  
  
     すべてのプログラミング要素に対してデータ型を指定することを、"*厳密な型指定*" と呼びます。 `Option Strict On` を設定すると、Visual Basic で厳密な型指定が適用されます。 次の理由により、これを強くお勧めします。  
  
    - これにより、変数とパラメーターの IntelliSense サポートが有効になります。 これにより、コードを入力しながら、プロパティとその他のメンバーを確認できます。  
  
    - これにより、コンパイラで型チェックを実行できます。 これは、オーバーフローなどのエラーによって、実行時に失敗する可能性があるステートメントをキャッチするのに役立ちます。 また、メソッドをサポートしていないオブジェクトに対するそれらの呼び出しもキャッチされます。  
  
    - これにより、コードの実行時間が短縮されます。 この理由の 1 つは、プログラミング要素のデータ型を指定しない場合、Visual Basic コンパイラによって `Object` 型が割り当てられることです。 コンパイルされたコードでは、`Object` とその他のデータ型との間で変換を行う必要がある場合があり、これによりパフォーマンスが低下します。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [Function プロシージャ](./function-procedures.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [再帰プロシージャ](./recursive-procedures.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [クラスとオブジェクト](../objects-and-classes/index.md)
- [オブジェクト指向プログラミング (Visual Basic)](../../concepts/object-oriented-programming.md)
