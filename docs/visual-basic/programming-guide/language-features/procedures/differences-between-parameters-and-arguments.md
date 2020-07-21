---
title: パラメーターと引数の違い
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- parameters [Visual Basic], and arguments
- procedure arguments
- Visual Basic code, procedures
- arguments [Visual Basic], and parameters
- procedure parameters
- parameters [Visual Basic], definition
ms.assetid: c237c056-74f4-4749-9f2c-15864f139a31
ms.openlocfilehash: dd0a62b6567f3e74763b7f2e9b96803c193c7976
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403357"
---
# <a name="differences-between-parameters-and-arguments-visual-basic"></a>パラメーターと引数の違い (Visual Basic)
ほとんどの場合、プロシージャには呼び出された状況に関する情報が必要です。 反復的なタスクや共有タスクを実行するプロシージャでは、呼び出しごとに異なる情報を使用します。 この情報は、呼び出し時にプロシージャに渡す変数、定数、式で構成されます。  
  
 この情報をプロシージャに伝えるために、プロシージャには "*パラメーター*" が定義されており、呼び出し元のコードからそのパラメーターに対して "*引数*" が渡されます。 パラメーターは駐車スペース、引数は自動車と考えることができます。 時間が異なれば、さまざまな自動車が 1 つの駐車スペースに駐車できるのと同じように、呼び出し元のコードからは、プロシージャを呼び出すたびに同じパラメーターに対して異なる引数を渡すことができます。  
  
## <a name="parameters"></a>パラメーター  
 "*パラメーター*" は、プロシージャを呼び出すときに渡す必要がある値を表します。 プロシージャの宣言でパラメーターを定義します。  
  
 `Function` または `Sub` プロシージャを定義するときは、プロシージャ名の直後にかっこで囲んだ "*パラメーター リスト*" を指定します。 パラメーターごとに、名前、データ型、および引渡し方法 ([ByVal](../../../language-reference/modifiers/byval.md) または [ByRef](../../../language-reference/modifiers/byref.md)) を指定します。 パラメーターが省略可能であることを示すこともできます。 これは、呼び出し元のコードから値を渡す必要がないことを意味します。  
  
 各パラメーターの名前は、プロシージャ内で "*ローカル変数*" として機能します。 パラメーター名は、他の変数を使用する場合と同じ方法で使用します。  
  
## <a name="arguments"></a>引数  
 "*引数*" は、プロシージャを呼び出すときにプロシージャ パラメーターに渡す値を表します。 呼び出し元のコードでは、プロシージャを呼び出すときに引数を指定します。  
  
 `Function` または `Sub` プロシージャを呼び出すときは、プロシージャ名の直後にかっこで囲んだ "*引数リスト*" を含めます。 各引数は、リスト内の同じ位置にあるパラメーターに対応しています。  
  
 パラメーターの定義とは異なり、引数には名前がありません。 各引数は式であり、0 個以上の変数、定数、およびリテラルを含めることができます。 評価される式のデータ型は、通常、対応するパラメーターに定義されているデータ型と一致する必要があり、いずれの場合でも、パラメーターの型に変換可能である必要があります。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [Function プロシージャ](./function-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [演算子プロシージャ](./operator-procedures.md)
- [方法: プロシージャのパラメーターを定義する](./how-to-define-a-parameter-for-a-procedure.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [再帰プロシージャ](./recursive-procedures.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
