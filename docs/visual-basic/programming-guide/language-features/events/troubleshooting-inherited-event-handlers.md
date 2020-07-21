---
title: 継承されたイベント ハンドラーのトラブルシューティング
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting events [Visual Basic]
- inherited events [Visual Basic]
- troubleshooting Visual Basic, event handlers
- event handling, troubleshooting
- event handlers, troubleshooting
ms.assetid: e1c8759f-5370-4308-8476-8c48b73509bf
ms.openlocfilehash: 4e7bedd1de5197fcf8b69091f4cc878f41b01cd5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405107"
---
# <a name="troubleshooting-inherited-event-handlers-in-visual-basic"></a>Visual Basic での継承されたイベント ハンドラーのトラブルシューティング
このトピックでは、継承されたコンポーネントのイベント ハンドラーで生じる一般的な問題を示します。  
  
## <a name="procedures"></a>プロシージャ  
  
#### <a name="code-in-event-handler-executes-twice-for-every-call"></a>呼び出しのたびにイベント ハンドラーのコードが 2 回実行される  
  
- 継承イベント ハンドラーには、[Handles](../../../language-reference/statements/handles-clause.md) 句を含めないでください。 基底クラスのメソッドは既にイベントに関連付けられており、適切に実行されます。 継承メソッドの `Handles` 句を削除してください。  
  
     [!code-vb[VbVbalrEvents#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#32)]  
  
- 継承メソッドに `Handles` キーワードを含めていない場合は、余計な [AddHandler ステートメント](../../../language-reference/statements/addhandler-statement.md)、または同じイベントを処理する別のメソッドが含まれていないことを確認してください。  
  
## <a name="see-also"></a>関連項目

- [イベント](index.md)
