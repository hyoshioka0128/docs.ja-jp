---
title: Throw ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Throw
helpviewer_keywords:
- structured exception handling, throw statements
- try-catch exception handling, throw statements
- throw statement [Visual Basic], about throw statements
- throwing exceptions, throw statement
- exception handling, throw statement
- On Error statement [Visual Basic], throwing exceptions
- throwing exceptions
- exception handling, unstructured
- throw statement [Visual Basic]
ms.assetid: a6e07406-5c8a-4498-87a2-8339f3651d62
ms.openlocfilehash: 95572b1739490e90f53da6b6ec283bfb532c46d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404136"
---
# <a name="throw-statement-visual-basic"></a>Throw ステートメント (Visual Basic)

プロシージャ内で例外をスローします。

## <a name="syntax"></a>構文

```vb
Throw [ expression ]
```

## <a name="part"></a>パーツ

`expression`\
スローされる例外に関する情報を提供します。 `Catch` ステートメント内に存在する場合は省略可能で、それ以外の場合は必須です。

## <a name="remarks"></a>Remarks

`Throw` ステートメントでは、構造化例外処理コード (`Try`...`Catch`...`Finally`) または非構造化例外処理コード (`On Error GoTo`) で処理できる例外をスローします。 `Throw` ステートメントを使用して、コード内でエラーをトラップできます。Visual Basic によって、適切な例外処理コードが見つかるまで呼び出し履歴が上に移動するためです。

式が指定されていない `Throw` ステートメントは、`Catch` ステートメントでのみ使用できます。この場合、ステートメントでは、現在 `Catch` ステートメントによって処理されている例外を再スローします。

`Throw` ステートメントによって、`expression` 例外の呼び出し履歴がリセットされます。 `expression` が指定されていない場合、呼び出し履歴は変更されません。 <xref:System.Exception.StackTrace%2A> プロパティによって、例外の呼び出し履歴にアクセスできます。

## <a name="example"></a>例

次のコードでは、`Throw` ステートメントを使用して、例外をスローしています。

[!code-vb[VbVbalrStatements#84](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#84)]

## <a name="see-also"></a>関連項目

- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
- [On Error ステートメント](on-error-statement.md)
