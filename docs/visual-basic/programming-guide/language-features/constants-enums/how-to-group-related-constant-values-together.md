---
title: '方法: 関連する定数値をまとめてグループ化する'
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic], constants
- constants [Visual Basic], grouping together
ms.assetid: 09d61da5-c940-4126-a79f-ba93c36653dc
ms.openlocfilehash: d2393af8b0c2b0c2e528f9908a78fbc7f182c8cf
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414441"
---
# <a name="how-to-group-related-constant-values-together-visual-basic"></a>方法: 関連する定数値をまとめてグループ化する (Visual Basic)
関連する定数をまとめてグループ化するには、列挙型が最適です。 列挙型は、クラスまたはモジュールの宣言セクションで `Enum` ステートメントを使用して作成します。 詳細については、[列挙型の宣言方法](how-to-declare-enumerations.md)に関するページを参照してください。  
  
### <a name="to-group-related-constant-values"></a>関連する定数値をグループ化するには  
  
1. コード アクセス レベル、`Enum` キーワード、有効な名前を含む宣言を記述します。 次の例では、`Private` の列挙型 `temperatureValues` を作成しています。  
  
     [!code-vb[VbEnumsTask#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#21)]  
  
2. 列挙型の定数を定義します。 次の例では、`Public` の `temperatureValues` 列挙型を作成して、値を割り当てています。  
  
     [!code-vb[VbEnumsTask#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [方法: 列挙型のメンバーを参照する](how-to-refer-to-an-enumeration-member.md)
- [列挙型を使用する状況](when-to-use-an-enumeration.md)
- [定数の概要](constants-overview.md)
- [定数とリテラルのデータ型](constant-and-literal-data-types.md)
- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
