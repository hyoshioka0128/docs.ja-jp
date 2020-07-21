---
title: '方法: 列挙型のメンバーを参照する'
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic], referring to
- values [Visual Basic], associating constant values with names
- enumeration members
- constants [Visual Basic], enumerated
ms.assetid: bbb5c3cc-7cdb-4814-8d6a-a6d91546ed1e
ms.openlocfilehash: 66c527bd4ba4721065de8fca8534fe652d0139be
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414415"
---
# <a name="how-to-refer-to-an-enumeration-member-visual-basic"></a>方法: 列挙型のメンバーを参照する (Visual Basic)
一連の関連する定数を操作する場合や、定数値に名前を関連付ける場合は、列挙型を使うと便利です。 たとえば、一連の整数型の定数を曜日に関連付けて列挙型として宣言すると、コードで整数値ではなく曜日名を使用することができます。  
  
 `Imports` ステートメントを使用することで、完全修飾名の使用を回避できます。 詳細については、[列挙型と名前の修飾](enumerations-and-name-qualification.md)に関するページを参照してください。  
  
### <a name="to-refer-to-an-enumeration-member"></a>列挙型のメンバーを参照するには  
  
- 列挙型でメンバー名を修飾します。 たとえば、次の例では、`FirstDayOfWeek` 列挙型の `Saturday` メンバーを変数 `DayValue` に割り当てています。  
  
     [!code-vb[VbEnumsTask#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#19)]  
  
## <a name="see-also"></a>関連項目

- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [方法: Visual Basic で列挙型を反復処理する](how-to-iterate-through-an-enumeration.md)
- [方法: 列挙値に関連付けられている文字列を確認する](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [列挙型を使用する状況](when-to-use-an-enumeration.md)
