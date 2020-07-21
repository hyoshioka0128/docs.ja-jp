---
title: '方法: 列挙値に関連付けられている文字列を確認する'
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
- strings [Visual Basic], enumeration values
- values [Visual Basic], enumeration members
ms.assetid: 9253e7c8-579c-49a2-8f26-392b20ea99eb
ms.openlocfilehash: 525da9206472afefa9f85b49ceee0775cbd168c3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414467"
---
# <a name="how-to-determine-the-string-associated-with-an-enumeration-value-visual-basic"></a>方法: 列挙値に関連付けられている文字列を確認する (Visual Basic)
<xref:System.Enum.GetValues%2A> メソッドと <xref:System.Enum.GetNames%2A> メソッドを使用することで、列挙型メンバーに関連付けられている文字列と値を確認できます。  
  
### <a name="to-determine-the-string-associated-with-an-enumeration"></a>列挙型に関連付けられている文字列を確認するには  
  
- 列挙型メンバーに関連付けられている文字列を取得するには、<xref:System.Enum.GetNames%2A> メソッドを使用します。 次の例では、列挙型 `flavorEnum` を宣言してから、各メンバーに関連付けられている文字列を <xref:System.Enum.GetNames%2A> メソッドにより表示します。  
  
     [!code-vb[VbEnumsTask#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Enum.GetValues%2A>
- <xref:System.Enum.GetNames%2A>
- <xref:System.Enum>
- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [方法: 列挙型のメンバーを参照する](how-to-refer-to-an-enumeration-member.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [方法: Visual Basic で列挙型を反復処理する](how-to-iterate-through-an-enumeration.md)
- [列挙型を使用する状況](when-to-use-an-enumeration.md)
- [Enum ステートメント](../../../language-reference/statements/enum-statement.md)
