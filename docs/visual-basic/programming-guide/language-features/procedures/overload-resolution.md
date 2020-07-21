---
title: Overload Resolution
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- overload resolution
- procedures [Visual Basic], overloading
- procedures [Visual Basic], calling
- procedure overloading [Visual Basic], overload resolution
- signatures [Visual Basic], procedure
- overloads [Visual Basic], resolution
ms.assetid: 766115d1-4352-45fb-859f-6063e0de0ec0
ms.openlocfilehash: bcb99ef3845c1ce3998dc9dc8d9f1d335515c0a9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364371"
---
# <a name="overload-resolution-visual-basic"></a>オーバーロードの解決法 (Visual Basic)
Visual Basic コンパイラは、複数のオーバーロードされたバージョンで定義されているプロシージャの呼び出しを検出したときに、呼び出すオーバーロードを決定する必要があります。 そのために、次の手順が実行されます。  
  
1. **アクセシビリティ。** 呼び出し元のコードから呼び出すことができないようにするためのアクセス レベルが設定されたオーバーロードが排除されます。  
  
2. **パラメーターの数。** 呼び出しで指定されているパラメーターとは異なる数のパラメーターが定義されているオーバーロードが排除されます。  
  
3. **パラメーターのデータ型。** コンパイラは、拡張メソッドよりもインスタンス メソッドを優先します。 プロシージャ呼び出しに一致させるために拡大変換のみを必要とするインスタンス メソッドが見つかった場合は、すべての拡張メソッドが破棄され、コンパイラはインスタンス メソッドの候補のみを使用して手順を続行します。 そのようなインスタンス メソッドが見つからない場合は、インスタンス メソッドと拡張メソッドの両方を使用して手順を続行します。  
  
     この手順では、呼び出し元の引数のデータ型を、オーバーロードで定義されたパラメーターの型に変換できないオーバーロードが排除されます。  
  
4. **縮小変換。** 呼び出し元の引数の型から定義されているパラメーターの型への縮小変換を必要とするオーバーロードが排除されます。 これは、型チェック スイッチ ([Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)) が `On` か `Off` かに関係なく適用されます。  
  
5. **最少の拡大変換。** コンパイラは、残りのオーバーロードをペアで検討します。 各ペアについて、定義されているパラメーターのデータ型を比較します。 一方のオーバーロードの型が、もう一方の対応する型にすべて拡大変換される場合、コンパイラは後者を排除します。 つまり、必要な拡大変換が最も少ないオーバーロードが保持されます。  
  
6. **単一の候補。** オーバーロードが引き続きペアで検討され、残りのオーバーロードが 1 つになったら、呼び出しがそのオーバーロードに解決されます。 コンパイラがオーバーロードを 1 つの候補に絞り込むことができない場合は、エラーが生成されます。  
  
 次の図は、一連のオーバーロードされたバージョンの中から呼び出すバージョンを決定するプロセスを示しています。  
  
 ![オーバーロード解決プロセスのフロー ダイアグラム](./media/overload-resolution/determine-overloaded-version.gif "オーバーロードされたバージョン間の解決")
  
 次の例は、このオーバーロード解決プロセスを示しています。  
  
 [!code-vb[VbVbcnProcedures#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#62)]  
  
 [!code-vb[VbVbcnProcedures#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#63)]  
  
 最初の呼び出しでは、最初の引数の型 (`Short`) が対応するパラメーターの型 (`Byte`) に縮小変換されるため、コンパイラは最初のオーバーロードを排除します。 次に、2 番目のオーバーロードの各引数の型 (`Short` と `Single`) は、3 番目のオーバーロードの対応する型 (`Integer` と `Single`) に拡大変換されるため、3 番目のオーバーロードが排除されます。 2 番目のオーバーロードは必要な拡大変換が少ないため、コンパイラはこれを呼び出しに使用します。  
  
 2 番目の呼び出しでは、コンパイラは縮小変換に基づいてオーバーロードのいずれかを排除することができません。 最初の呼び出しと同じ理由で、3 番目のオーバーロードが排除されます。引数の型の拡大変換が少ない 2 番目のオーバーロードを呼び出すことができるためです。 ただし、コンパイラは最初と 2 番目のオーバーロード間で解決することはできません。 それぞれ、もう一方の対応する型に拡大変換されるパラメーターの型が定義されています (`Byte` から `Short`、`Single` から `Double`)。 そのため、コンパイラはオーバーロード解決エラーを生成します。  
  
## <a name="overloaded-optional-and-paramarray-arguments"></a>オーバーロードされた Optional および ParamArray 引数  
 最後のパラメーターが一方では [Optional](../../../language-reference/modifiers/optional.md)、もう一方では [ParamArray](../../../language-reference/modifiers/paramarray.md) として宣言されている点を除き、プロシージャの 2 つのオーバーロードが同じシグネチャを持つ場合、コンパイラはそのプロシージャの呼び出しを次のように解決します。  
  
|呼び出しで指定されている最後の引数|コンパイラは、最後の引数を次のように宣言するオーバーロードに呼び出しを解決する|  
|---|---|  
|値なし (引数を省略)|`Optional`|  
|単一の値|`Optional`|  
|コンマ区切りリストの 2 つ以上の値|`ParamArray`|  
|任意の長さの配列 (空の配列を含む)|`ParamArray`|  
  
## <a name="see-also"></a>関連項目

- [省略可能なパラメーター](./optional-parameters.md)
- [パラメーター配列](./parameter-arrays.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [プロシージャのトラブルシューティング](./troubleshooting-procedures.md)
- [方法: プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)
- [方法: オーバーロードされたプロシージャを呼び出す](./how-to-call-an-overloaded-procedure.md)
- [方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)
- [Overloads](../../../language-reference/modifiers/overloads.md)
- [拡張メソッド](./extension-methods.md)
