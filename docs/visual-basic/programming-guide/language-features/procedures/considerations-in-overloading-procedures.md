---
title: プロシージャのオーバーロードに関する注意事項
ms.date: 07/20/2015
helpviewer_keywords:
- signatures [Visual Basic], ParamArray arguments
- ParamArray keyword [Visual Basic], parameter arrays
- ParamArray keyword [Visual Basic], arguments and signatures
- function overloading [Visual Basic], implicit overloads for ParamArray
- ParamArray keyword [Visual Basic], signatures
- Visual Basic code, procedures
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], overloading
- parameters [Visual Basic], lists
- function overloading [Visual Basic], typeless programming
- typeless programming
- function overloading [Visual Basic], restrictions
- arguments [Visual Basic], optional
- optional arguments [Visual Basic], overloading
- signatures [Visual Basic], procedure
- parameter lists [Visual Basic]
- parameter arrays [Visual Basic], overloading arguments
- Visual Basic code, parameter lists
- procedure overloading [Visual Basic], considerations
- Option Explicit statement [Visual Basic]
- restrictions [Visual Basic], overloading procedures
- procedures [Visual Basic], parameter lists
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
ms.openlocfilehash: c4075c87df8b9daa56ca1d35e0d6661598895fdc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403370"
---
# <a name="considerations-in-overloading-procedures-visual-basic"></a>プロシージャのオーバーロードに関する注意事項 (Visual Basic)
プロシージャをオーバーロードするときは、オーバーロードされたバージョンごとに異なる "*シグネチャ*" を使用する必要があります。 通常、これはバージョンごとに異なるパラメーター リストを指定する必要があることを意味します。 詳細については、「[プロシージャのオーバーロード](./procedure-overloading.md)」の「異なるシグネチャ」をご覧ください。  
  
 シグネチャが異なるという前提で、`Function` プロシージャを `Sub` プロシージャでオーバーロードすることができ、その逆も可能です。 一方に戻り値があり、もう一方にはないという点だけでは、2 つのオーバーロードが異なると見なすことはできません。  
  
 プロパティは、プロシージャをオーバーロードする場合と同じ方法で、同じ制限を適用してオーバーロードすることができます。 ただし、プロパティでプロシージャをオーバーロードすることはできません。その逆も同様です。  
  
## <a name="alternatives-to-overloaded-versions"></a>オーバーロードされたバージョンの代替  
 特に、引数が省略可能である場合やその数が可変である場合は、オーバーロードされたバージョンに代わるものを使用することがあります。  
  
 省略可能な引数はすべての言語で必ずしもサポートされているわけではなく、パラメーター配列は Visual Basic に限定されていることに注意してください。 さまざまな言語のいずれかで記述されたコードから呼び出される可能性が高いプロシージャを作成する場合は、オーバーロードされたバージョンが最も優れた柔軟性を提供します。  
  
### <a name="overloads-and-optional-arguments"></a>オーバーロードと省略可能な引数  
 呼び出し元のコードが、1 つ以上の引数を必要に応じて指定または省略できる場合は、複数のオーバーロードされたバージョンを定義することも、省略可能なパラメーターを使用することもできます。  
  
#### <a name="when-to-use-overloaded-versions"></a>オーバーロードされたバージョンを使用する場合  
 次の場合は、一連のオーバーロードされたバージョンを定義することを検討してください。  
  
- 呼び出し元のコードが省略可能な引数を指定するかどうかによって、プロシージャ コードのロジックが大きく異なる場合。  
  
- プロシージャ コードで、呼び出し元のコードが省略可能な引数を指定しているかどうかを確実にテストすることができない場合。 たとえば、呼び出し元のコードが指定することを期待できない既定値の候補が存在しない場合は、これに該当します。  
  
#### <a name="when-to-use-optional-parameters"></a>省略可能なパラメーターを使用する場合  
 次の場合には、1 つ以上の省略可能なパラメーターを使用することをお勧めします。  
  
- 呼び出し元のコードが省略可能な引数を指定しない場合に必要な唯一のアクションが、パラメーターを既定値に設定することである場合。 このような場合、1 つ以上の `Optional` パラメーターを持つ単一のバージョンを定義すると、プロシージャー コードの複雑さを軽減できます。  
  
 詳細については、「[省略可能なパラメーター](./optional-parameters.md)」をご覧ください。  
  
### <a name="overloads-and-paramarrays"></a>オーバーロードと ParamArray  
 呼び出し元のコードが可変数の引数を渡すことができる場合は、複数のオーバーロードされたバージョンを定義することも、パラメーター配列を使用することもできます。  
  
#### <a name="when-to-use-overloaded-versions"></a>オーバーロードされたバージョンを使用する場合  
 次の場合は、一連のオーバーロードされたバージョンを定義することを検討してください。  
  
- 呼び出し元のコードがパラメーター配列に渡す値が常に少数であることがわかっている場合。  
  
- 呼び出し元のコードが渡す値の数によって、プロシージャ コードのロジックが大きく異なる場合。  
  
- 呼び出し元のコードがさまざまなデータ型の値を渡すことができる場合。  
  
#### <a name="when-to-use-a-parameter-array"></a>パラメーター配列を使用する場合  
 次の場合は、`ParamArray` パラメーターの方が適しています。  
  
- 呼び出し元のコードがパラメーター配列に渡すことができる値の数を予測できず、数が多くなる可能性がある場合。  
  
- プロシージャのロジックが、すべての値に対して基本的に同じ操作を実行するものであり、呼び出し元のコードから渡されるすべての値を反復処理するのに適している場合。  
  
 詳細については、「[パラメーター配列](./parameter-arrays.md)」をご覧ください。  
  
## <a name="implicit-overloads-for-optional-parameters"></a>Optional パラメーターの暗黙的なオーバーロード  
 [Optional](../../../language-reference/modifiers/optional.md) パラメーターを持つプロシージャは、省略可能なパラメーターを持つものと持たないものの 2 つのオーバーロードされたプロシージャと同等です。 これらのいずれかに対応するパラメーター リストでこのようなプロシージャをオーバーロードすることはできません。 次の宣言はこれを示しています。  
  
 [!code-vb[VbVbcnProcedures#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#58)]  
  
 [!code-vb[VbVbcnProcedures#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#60)]  
  
 [!code-vb[VbVbcnProcedures#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#61)]  
  
 複数の省略可能なパラメーターを持つプロシージャでは、前の例と同様のロジックで到達する一連の暗黙的なオーバーロードがあります。  
  
## <a name="implicit-overloads-for-a-paramarray-parameter"></a>ParamArray パラメーターの暗黙的なオーバーロード  
 コンパイラは、[ParamArray](../../../language-reference/modifiers/paramarray.md) パラメーターを持つプロシージャを、次のように、呼び出し元のコードがパラメーター配列に渡す内容が相互に異なる無数のオーバーロードを持つものと見なします。  
  
- 呼び出し元のコードが `ParamArray` に引数を指定しない場合に対応する 1 つのオーバーロード  
  
- 呼び出し元のコードが `ParamArray` 要素型の 1 次元配列を指定した場合に対応する 1 つのオーバーロード  
  
- すべての正の整数について、呼び出し元のコードがその数の引数を各 `ParamArray` 要素型に指定した場合に対応する 1 つのオーバーロード  
  
 次の宣言は、これらの暗黙的なオーバーロードを示しています。  
  
 [!code-vb[VbVbcnProcedures#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#68)]  
  
 [!code-vb[VbVbcnProcedures#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#70)]  
  
 パラメーター配列に対して 1 次元配列を受け取るパラメーター リストでそのようなプロシージャをオーバーロードすることはできません。 ただし、他の暗黙的なオーバーロードのシグネチャを使用できます。 次の宣言はこれを示しています。  
  
 [!code-vb[VbVbcnProcedures#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#71)]  
  
## <a name="typeless-programming-as-an-alternative-to-overloading"></a>オーバーロードの代替手段としての型宣言を省略したプログラミング  
 呼び出し元のコードがパラメーターにさまざまなデータ型を渡すことができるようにする場合、別の方法として、型宣言を省略したプログラミングがあります。 [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)または [-optionstrict](../../../reference/command-line-compiler/optionstrict.md) コンパイラ オプションで、型チェック スイッチを `Off` に設定できます。 その後、パラメーターのデータ型を宣言する必要はありません。 ただし、オーバーロードと比較して、この方法には次の欠点があります。  
  
- 型宣言を省略したプログラミングでは、効率的ではない実行コードが生成されます。  
  
- プロシージャは、渡されることが予想されるすべてのデータ型をテストする必要があります。  
  
- 呼び出し元のコードが、プロシージャでサポートされていないデータ型を渡した場合、コンパイラはエラーを通知できません。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [プロシージャのトラブルシューティング](./troubleshooting-procedures.md)
- [方法: プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)
- [方法: オーバーロードされたプロシージャを呼び出す](./how-to-call-an-overloaded-procedure.md)
- [方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [オーバーロードの解決](./overload-resolution.md)
- [Overloads](../../../language-reference/modifiers/overloads.md)
