---
title: '方法: 値を返さないプロシージャを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- procedure calls [Visual Basic], returning values
- Visual Basic code, procedures
- procedures [Visual Basic], calling
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
ms.openlocfilehash: 514d6e576b9b782387840ae04dcefa00de876aa9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388739"
---
# <a name="how-to-call-a-procedure-that-does-not-return-a-value-visual-basic"></a>方法: 値を返さないプロシージャを呼び出す (Visual Basic)
`Sub` プロシージャから呼び出し元コードに対しては値が返されません。 これは、スタンドアロンの呼び出し元ステートメントを使用して明示的に呼び出します。 式内でその名前を使用するだけでは呼び出せません。  
  
### <a name="to-call-a-sub-procedure"></a>Sub プロシージャを呼び出すには  
  
1. `Sub` プロシージャの名前を指定します。  
  
2. プロシージャ名の後にかっこを使用して引数リストを囲みます。 引数がない場合は、必要に応じてかっこを省略できます。 ただし、かっこを使用すると、コードが読みやすくなります。  
  
3. 引数リストの引数をコンマで区切ってかっこ内に配置します。 引数の指定は必ず、`Sub` プロシージャで定義されている対応するパラメーターと同じ順序で行ってください。  
  
     次の例では、Visual Basic <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> 関数を呼び出して、アプリケーション ウィンドウをアクティブにします。 <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> は、ウィンドウ タイトルを唯一の引数として受け取ります。 呼び出し元のコードには値が返されません。 メモ帳プロセスが実行されていない場合、この例では <xref:System.ArgumentException> がスローされます。 `Shell` プロシージャでは、アプリケーションが指定されたパスにあることを前提としています。  
  
     [!code-vb[VbVbalrCatRef#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCatRef/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Interaction.Shell%2A>
- <xref:System.ArgumentException>
- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Sub ステートメント](../../../language-reference/statements/sub-statement.md)
- [方法: プロシージャを作成する](./how-to-create-a-procedure.md)
- [方法: 値を返すプロシージャを呼び出す](./how-to-call-a-procedure-that-returns-a-value.md)
- [方法: Visual Basic でイベント ハンドラーを呼び出す](./how-to-call-an-event-handler.md)
