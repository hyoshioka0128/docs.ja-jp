---
title: 構造体メンバーとして宣言された配列を初期サイズで宣言することはできません。
ms.date: 07/20/2015
f1_keywords:
- vbc31043
- bc31043
helpviewer_keywords:
- BC31043
ms.assetid: 5bd90c71-1b78-444b-91e1-4789451ef085
ms.openlocfilehash: de9d77aa9ea853b6f044e91878044115588ca77c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701245"
---
# <a name="arrays-declared-as-structure-members-cannot-be-declared-with-an-initial-size"></a>構造体メンバーとして宣言された配列を初期サイズで宣言することはできません。
構造体の配列が初期サイズで宣言されています。 構造体要素を初期化することはできません。また、配列サイズの宣言は初期化の1つの形式です。  
  
 **エラー ID:** BC31043  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 構造体の配列を動的として定義します (初期サイズはありません)。  
  
2. 配列の特定のサイズが必要な場合は、コードの実行時に[ReDim ステートメント](../../../visual-basic/language-reference/statements/redim-statement.md)を使用して動的配列を再作成できます。 次に例を示します。  
  
    ```vb  
    Structure demoStruct  
        Public demoArray() As Integer  
    End Structure  
    Sub useStruct()  
        Dim struct As demoStruct  
        ReDim struct.demoArray(9)  
        Struct.demoArray(2) = 777  
    End Sub  
    ```  
  
## <a name="see-also"></a>関連項目

- [配列](../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [2 つのオブジェクトが等しいかどうかをテストする方法構造体を宣言する](../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)
