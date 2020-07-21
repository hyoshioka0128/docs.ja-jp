---
title: Alias 句
ms.date: 07/20/2015
f1_keywords:
- vb.Alias
helpviewer_keywords:
- Alias keyword [Visual Basic]
ms.assetid: 58c06b11-465d-4d87-906a-73200a3d7f19
ms.openlocfilehash: c28e931a376b20b2058a7187551405cd9523d4fe
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408472"
---
# <a name="alias-clause-visual-basic"></a>Alias 句 (Visual Basic)
外部プロシージャがその DLL で別の名前を使用することを示します。  
  
## <a name="remarks"></a>Remarks  
 `Alias` キーワードは次のコンテキストで使用できます。  
  
 [Declare ステートメント](declare-statement.md)  
  
 次の例では、`Alias` キーワードを使用して、advapi32.dll 内の関数の名前 `GetUserNameA` を指定しています。この例では代わりに `getUserName` が使用されています。 関数 `getUserName` はサブ `getUser` で呼び出され、それによって現在のユーザーの名前が表示されます。  
  
 [!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>関連項目

- [キーワード](../keywords/index.md)
