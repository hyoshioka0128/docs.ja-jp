---
title: ジェネリック プロシージャ
ms.date: 07/20/2015
helpviewer_keywords:
- generic methods [Visual Basic], type inference
- generics [Visual Basic], type inference
- procedures [Visual Basic], generic
- generic procedures
- type inference, generics
- generic methods [Visual Basic]
- type inference
- generics [Visual Basic], procedures
- generic procedures [Visual Basic], type inference
ms.assetid: 95577b28-137f-4d5c-a149-919c828600e5
ms.openlocfilehash: 2efc0410b9d4bb663e1ff19d5a5456d7ff2c99bd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394066"
---
# <a name="generic-procedures-in-visual-basic"></a>Visual Basic におけるジェネリック プロシージャ
"*ジェネリック プロシージャ*" は、"*ジェネリック メソッド*" とも呼ばれる、少なくとも 1 つの型パラメーターを含むように定義されたプロシージャです。 これによって、呼び出し元のコードが、プロシージャを呼び出すたびに、要件に合わせてデータ型を調整できるようになります。  
  
 プロシージャは、ジェネリック クラスまたはジェネリック構造体内で定義されているというだけの理由ではジェネリックになりません。 プロシージャがジェネリックになるためには、通常のパラメーター以外に、少なくとも 1 つの型パラメーターを受け取る必要があります。 ジェネリックのクラスまたは構造体に非ジェネリック プロシージャを含めることができます。また、非ジェネリックのクラス、構造体、またはモジュールにジェネリック プロシージャを含めることができます。  
  
 ジェネリック プロシージャは、通常のパラメーター リスト、戻り値の型 (存在する場合)、およびプロシージャ コード内で、その型パラメーターを使用できます。  
  
## <a name="type-inference"></a>型推論  
 型引数をまったく指定せずにジェネリック プロシージャを呼び出すことができます。 このように呼び出した場合、コンパイラが、プロシージャの型引数に渡す適切なデータ型を決定しようとします。 これは "*型の推定*" と呼ばれます。 次のコードに示す呼び出しでは、型 `String` を型パラメーター `t` に渡す必要があるとコンパイラによって推定されます。  
  
 [!code-vb[VbVbalrDataTypes#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#15)]  
  
 コンパイラが、呼び出しのコンテキストから型引数を推定できない場合、エラーを報告します。 このようなエラーの原因の 1 つとして、配列のランクの不一致が考えられます。 たとえば、通常のパラメーターを型パラメーターの配列として定義するとします。 呼び出すジェネリック プロシージャによって異なるランク (次元数) の配列が提供されると、不一致のために型の推定が失敗します。 次のコードに示す呼び出しでは、1 次元配列を予期しているプロシージャに 2 次元配列が渡されます。  
  
```vb  
Public Sub demoSub(Of t)(ByVal arg() As t)
End Sub

Public Sub callDemoSub()
    Dim twoDimensions(,) As Integer
    demoSub(twoDimensions)
End Sub
```
  
 型の推定を呼び出すことができるのは、すべての型引数を省略した場合のみです。 型引数を 1 つ指定する場合は、すべて指定する必要があります。  
  
 型の推定は、ジェネリック プロシージャでのみサポートされています。 ジェネリック クラス、構造体、インターフェイス、またはデリゲートに対して、型の推定を呼び出すことはできません。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、配列内の特定の要素を探す、ジェネリック `Function` プロシージャを定義しています。 1 つの型パラメーターを定義し、それを使用してパラメーター リスト内の 2 つのパラメーターを構築します。  
  
### <a name="code"></a>コード  
 [!code-vb[VbVbalrDataTypes#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#14)]  
  
### <a name="comments"></a>コメント  
 前の例は、`searchArray` の各要素に対して `searchValue` を比較する必要があります。 この動作を保証するために、型パラメーター `T` が <xref:System.IComparable%601> インターフェイスを実装するように制約します。 コードは、<xref:System.IComparable%601.CompareTo%2A> メソッドを `=` 演算子の代わりに使用します。`T` に提供される型引数で `=` 演算子がサポートされる保証がないためです。  
  
 次のコードを使用して `findElement` プロシージャをテストできます。  
  
 [!code-vb[VbVbalrDataTypes#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#13)]  
  
 上記の `MsgBox` の呼び出しで、それぞれ "0"、"1"、および "-1" が表示されます。  
  
## <a name="see-also"></a>関連項目

- [Generic Types in Visual Basic](generic-types.md)
- [方法: 複数のデータ型に同一の機能を提供できるクラスを定義する](how-to-define-a-class-that-can-provide-identical-functionality.md)
- [方法: ジェネリック クラスを使用する](how-to-use-a-generic-class.md)
- [手順](../procedures/index.md)
- [プロシージャのパラメーターと引数](../procedures/procedure-parameters-and-arguments.md)
- [型リスト](../../../language-reference/statements/type-list.md)
- [パラメーター リスト](../../../language-reference/statements/parameter-list.md)
