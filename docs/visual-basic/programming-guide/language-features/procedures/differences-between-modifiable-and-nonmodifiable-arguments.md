---
title: 変更できる引数と変更できない引数の違い
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedure arguments
- arguments [Visual Basic], nonmodifiable
- Visual Basic code, procedures
- arguments [Visual Basic], modifiable
ms.assetid: 87b2df69-e1f7-4657-9caf-b3f48d693428
ms.openlocfilehash: 733f92cc2cdaa6e923c57649774ceb64de172c18
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403344"
---
# <a name="differences-between-modifiable-and-nonmodifiable-arguments-visual-basic"></a>変更できる引数と変更できない引数の違い (Visual Basic)
プロシージャを呼び出す場合、通常は 1 つ以上の引数を渡します。 各引数は、基となるプログラミング要素に対応します。 基となる要素と引数自体のいずれも、変更可能な場合と変更不可能な場合があります。  
  
## <a name="modifiable-and-nonmodifiable-elements"></a>変更可能な要素と変更不可能な要素  
 プログラミング要素は、値を変更できる "*変更可能な要素*"、または作成後は固定値を持つ "*変更不可能な要素*" のいずれかの場合があります。  
  
 次の表に、変更可能なプログラミング要素と変更不可能なプログラミング要素を示します。  
  
|変更可能な要素|変更不可能な要素|  
|-------------------------|----------------------------|  
|オブジェクト変数を含むローカル変数 (プロシージャ内で宣言) (読み取り専用を除く)|読み取り専用の変数、フィールド、プロパティ|  
|フィールド (モジュール、クラス、構造体のメンバー変数) (読み取り専用を除く)|定数とリテラル|  
|プロパティ (読み取り専用を除く)|列挙メンバー|  
|配列要素|式 (要素が変更可能な場合でも)|  
  
## <a name="modifiable-and-nonmodifiable-arguments"></a>変更可能な引数と変更不可能な引数  
 "*変更可能な引数*" とは、基となる要素が変更可能なものです。 呼び出し元のコードにはいつでも新しい値を格納できます。引数 [ByRef](../../../language-reference/modifiers/byref.md) を渡すと、プロシージャのコードによって呼び出し元のコードの基となる要素を変更することもできます。  
  
 "*変更不可能な引数*" には、変更不可能な基となる要素があるか、[ByVal](../../../language-reference/modifiers/byval.md) が渡されます。 変更可能な要素であっても、プロシージャを使用して、呼び出し元のコードの基となる要素を変更することはできません。 変更不可能な要素の場合、呼び出し元のコード自体でそれを変更することはできません。  
  
 呼び出されたプロシージャによって、変更不可能な引数のローカル コピーを変更することはできますが、その変更は呼び出し元のコードの基となる要素には影響しません。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [引数の値渡しと参照渡しの違い](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [方法: プロシージャ引数の値を変更する](./how-to-change-the-value-of-a-procedure-argument.md)
- [方法: プロシージャ引数の値が変更されないように保護する](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
