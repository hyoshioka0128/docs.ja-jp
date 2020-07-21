---
title: '方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], parameters
- procedure overloading [Visual Basic], optional parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
ms.assetid: 825f9d56-4cde-43fd-993a-b9171717e2eb
ms.openlocfilehash: 9ae6818b1e03ccd00ed554e98690e02ffa45de99
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387843"
---
# <a name="how-to-overload-a-procedure-that-takes-optional-parameters-visual-basic"></a>方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする (Visual Basic)
プロシージャに 1 つ以上の [Optional](../../../language-reference/modifiers/optional.md) パラメーターがある場合、暗黙的なオーバーロードのいずれかに一致するオーバーロードされたバージョンを定義することはできません。 詳細については、「[プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)」の「Optional パラメーターの暗黙的なオーバーロード」をご覧ください。  
  
## <a name="one-optional-parameter"></a>1 つの省略可能なパラメーター  
  
#### <a name="to-overload-a-procedure-that-takes-one-optional-parameter"></a>1 つの省略可能なパラメーターを受け取るプロシージャをオーバーロードするには  
  
1. パラメーター リストに省略可能なパラメーターが含まれた、`Sub` または `Function` 宣言ステートメントを記述します。 このオーバーロードされたバージョンでは、`Optional` キーワードは使用しないでください。  
  
2. `Sub` または `Function` キーワードの前に [Overloads](../../../language-reference/modifiers/overloads.md) キーワードを指定します。  
  
3. 呼び出し元のコードで省略可能な引数が指定されたときに実行する必要があるプロシージャ コードを記述します。  
  
4. プロシージャを、必要に応じて `End Sub` または `End Function` ステートメントで終了します。  
  
5. パラメーター リストに省略可能なパラメーターが含まれていない点を除いて、最初の宣言と同じである 2 番目の宣言ステートメントを記述します。  
  
6. 呼び出し元のコードで省略可能な引数が指定されないときに実行する必要があるプロシージャ コードを記述します。 プロシージャを、必要に応じて `End Sub` または `End Function` ステートメントで終了します。  
  
     次の例は、省略可能なパラメーターで定義されたプロシージャ、2 つのオーバーロードされたプロシージャの同等のセット、無効および有効なオーバーロードされたバージョンの例を示しています。  
  
     [!code-vb[VbVbcnProcedures#59](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#59)]  
  
     [!code-vb[VbVbcnProcedures#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#60)]  
  
     [!code-vb[VbVbcnProcedures#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#61)]  
  
## <a name="multiple-optional-parameters"></a>複数の省略可能なパラメーター  
 複数の省略可能なパラメーターがあるプロシージャでは、通常、3 つ以上のオーバーロードされたバージョンが必要です。 たとえば、2 つの省略可能なパラメーターがあり、呼び出し元のコードが各パラメーターを相互に独立して指定または省略できる場合、4 つのオーバーロードされたバージョン (指定された引数の可能な組み合わせごとに 1 つ) が必要です。  
  
 省略可能なパラメーターの数が増えると、オーバーロードの複雑さが増します。 指定された引数の一部の組み合わせが許容されない場合を除き、N 個の省略可能なパラメーターには 2 ^ N 個のオーバーロードされたバージョンが必要となります。 プロシージャの性質によっては、オーバーロードされたバージョンをすべて定義することによってロジックが明確になることから、余分な労力をかけるだけの価値がある場合もあります。  
  
#### <a name="to-overload-a-procedure-that-takes-more-than-one-optional-parameter"></a>複数の省略可能なパラメーターを受け取るプロシージャをオーバーロードするには  
  
1. プロシージャのロジックで許容される、指定された省略可能な引数の組み合わせを特定します。 ある省略可能なパラメーターが別の省略可能なパラメーターに依存する場合、許容されない組み合わせが生じる可能性があります。 たとえば、あるパラメーターが個人の名前を受け入れ、別のパラメーターがその個人の年齢を受け入れる場合、年齢を指定し、名前を省略する引数の組み合わせは許容されません。  
  
2. 指定された省略可能な引数の許容される組み合わせごとに、対応するパラメーター リストを定義する、`Sub` または `Function` 宣言ステートメントを記述します。 `Optional` キーワードは使用しないでください。  
  
3. 各宣言で、`Sub` または `Function` キーワードの前に [Overloads](../../../language-reference/modifiers/overloads.md) キーワードを指定します。  
  
4. 各宣言の後に、呼び出し元のコードでその宣言のパラメーター リストに対応する引数リストが指定されたときに実行する必要があるプロシージャ コードを記述します。  
  
5. 各プロシージャを、必要に応じて `End Sub` または `End Function` ステートメントで終了します。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [省略可能なパラメーター](./optional-parameters.md)
- [パラメーター配列](./parameter-arrays.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [プロシージャのトラブルシューティング](./troubleshooting-procedures.md)
- [方法: プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)
- [方法: オーバーロードされたプロシージャを呼び出す](./how-to-call-an-overloaded-procedure.md)
- [方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [オーバーロードの解決](./overload-resolution.md)
