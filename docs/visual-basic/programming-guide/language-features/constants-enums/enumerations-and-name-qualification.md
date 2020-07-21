---
title: 列挙型と名前の修飾
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], enumerations
- Imports statement [Visual Basic], namespace declarations
- declaring namespaces [Visual Basic], enumerations
- name collisions
- ambiguous names [Visual Basic], enumerations
- enumerations [Visual Basic], name qualification
- names [Visual Basic], avoiding conflicts
- namespaces [Visual Basic], declaring
- naming conflicts, enumerations
- naming conflicts, qualifying names
- declaring enumerations
- references [Visual Basic], enumeration members
- naming conventions [Visual Basic], naming conflicts
- declarations [Visual Basic], namespaces
ms.assetid: 08ba2738-df52-4140-bc55-f57c871c9b73
ms.openlocfilehash: 4b09284b8282c481e406050d37cbdb2f3c8686bc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414506"
---
# <a name="enumerations-and-name-qualification-visual-basic"></a>列挙型と名前修飾 (Visual Basic)
通常、列挙型のメンバーを参照する場合は、列挙型名でメンバー名を修飾する必要があります。 たとえば、`Days` 列挙型の `Sunday` メンバーを参照するには次の構文を使用します。  
  
 [!code-vb[VbEnumsTask#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#18)]  
  
## <a name="using-the-imports-statement"></a>Imports ステートメントを使用する  
 次の例に示すように、`Imports` ステートメントを名前空間の宣言セクションに追加すれば、完全修飾名を使わずに済みます。  
  
 [!code-vb[VbEnumsTask#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#22)]  
  
 `Imports` ステートメントは、参照先のプロジェクトとアセンブリの名前空間名、およびこのステートメントが出現するモジュールと同じプロジェクトに含まれる名前空間名をインポートします。 このステートメントを追加すると、次の例に示すように、修飾を行うことなく列挙型メンバーを参照できるようになります。  
  
 [!code-vb[VbEnumsTask#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#24)]  
  
 関連する定数一式を列挙型にまとめることで、異なるコンテキストで同じ定数名を使用できます。 たとえば、`Days` 列挙型と `WorkDays` 列挙型の平日を表す定数に同じ名前を使用可能です。 列挙型と共に `Imports` ステートメントを使用する場合は、あいまいな参照を行わないように注意してください。 次に例を示します。  
  
 [!code-vb[VbEnumsTask#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#22)]  
  
 [!code-vb[VbEnumsTask#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#25)]  
  
 `Monday` が `Days` 列挙型と `Workdays` 列挙型の両方のメンバーである場合、このコードではコンパイラ エラーが発生します。 あいまいな参照を使うことなく各定数を参照するには、定数名をその列挙型で修飾します。 次のコードでは、`Days` 列挙型と `WorkDays` 列挙型の `Saturday` 定数を参照しています。  
  
 [!code-vb[VbEnumsTask#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#32)]  
  
## <a name="see-also"></a>関連項目

- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [方法: 列挙型のメンバーを参照する](how-to-refer-to-an-enumeration-member.md)
- [方法: Visual Basic で列挙型を反復処理する](how-to-iterate-through-an-enumeration.md)
- [方法: 列挙値に関連付けられている文字列を確認する](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [列挙型を使用する状況](when-to-use-an-enumeration.md)
- [定数とリテラルのデータ型](constant-and-literal-data-types.md)
- [Enum ステートメント](../../../language-reference/statements/enum-statement.md)
- [Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [データの種類](../../../language-reference/data-types/index.md)
