---
title: '方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], parameters
- procedure overloading [Visual Basic], indefinite number of parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
ms.assetid: c7042de2-2422-4039-94e8-ac298896af69
ms.openlocfilehash: ddff8c8cd82593b7d89fb0847e56123c287e364b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387882"
---
# <a name="how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters-visual-basic"></a>方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする (Visual Basic)
プロシージャに [ParamArray](../../../language-reference/modifiers/paramarray.md) パラメーターが含まれている場合、パラメーター配列に対して 1 次元配列を受け取るオーバーロードされたバージョンを定義することはできません。 詳細については、「[プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)」の「ParamArray パラメーターの暗黙的なオーバーロード」をご覧ください。  
  
### <a name="to-overload-a-procedure-that-takes-a-variable-number-of-parameters"></a>可変数のパラメーターを受け取るプロシージャをオーバーロードするには  
  
1. `ParamArray` パラメーターよりもオーバーロードされたバージョンの方が、プロシージャと呼び出し元のコードのロジックに多くのメリットがもたらされることを確認します。 「[プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)」の「オーバーロードと ParamArray」をご覧ください。  
  
2. プロシージャがパラメーター リストの変数部分で受け入れる必要がある、指定される値の数を決定します。 これには、値がないケースが含まれる場合や、単一の 1 次元配列のケースが含まれる場合があります。  
  
3. 指定される値の許容数ごとに、対応するパラメーター リストを定義する `Sub` または `Function` 宣言ステートメントを記述します。 このオーバーロードされたバージョンでは、`Optional` または `ParamArray` キーワードは使用しないでください。  
  
4. 各宣言で、`Sub` または `Function` キーワードの前に [Overloads](../../../language-reference/modifiers/overloads.md) キーワードを指定します。  
  
5. 各宣言の後に、呼び出し元のコードでその宣言のパラメーター リストに対応する値が指定されたときに実行する必要があるプロシージャ コードを記述します。  
  
6. 各プロシージャを、必要に応じて `End Sub` または `End Function` ステートメントで終了します。  
  
## <a name="example"></a>例  
 次の例は、[ParamArray](../../../language-reference/modifiers/paramarray.md) パラメーターを使用して定義されたプロシージャと、これと同等の一連のオーバーロードされたプロシージャを示しています。  
  
 [!code-vb[VbVbcnProcedures#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#69)]  
  
 [!code-vb[VbVbcnProcedures#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#70)]  
  
 パラメーター配列に対して 1 次元配列を受け取るパラメーター リストでそのようなプロシージャをオーバーロードすることはできません。 ただし、他の暗黙的なオーバーロードのシグネチャを使用できます。 次の宣言はこれを示しています。  
  
 [!code-vb[VbVbcnProcedures#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#71)]  
  
 オーバーロードされたバージョンのコードでは、呼び出し元のコードで `ParamArray` パラメーターに 1 つ以上の値が指定されたかどうかをテストしたり、指定された場合にその数をテストしたりする必要はありません。 Visual Basic は、呼び出し元の引数リストと一致するバージョンに制御を渡します。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 `ParamArray` パラメーターを使用したプロシージャは、一連のオーバーロードされたバージョンと同等であるため、これらの暗黙的なオーバーロードのいずれかに対応するパラメーター リストでそのようなプロシージャをオーバーロードすることはできません。 詳細については、「[プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)」をご覧ください。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 無限に大きくなる可能性がある配列を処理する場合は常に、アプリケーションの何らかの内部容量が超過するリスクがあります。 パラメーター配列を受け入れる場合は、呼び出し元のコードから渡された配列の長さをテストし、それがアプリケーションにとって大きすぎる場合は、適切な措置を講じる必要があります。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [省略可能なパラメーター](./optional-parameters.md)
- [パラメーター配列](./parameter-arrays.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [プロシージャのトラブルシューティング](./troubleshooting-procedures.md)
- [方法: プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)
- [方法: オーバーロードされたプロシージャを呼び出す](./how-to-call-an-overloaded-procedure.md)
- [方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [オーバーロードの解決](./overload-resolution.md)
