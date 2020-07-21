---
title: '方法: プロパティ プロシージャを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- Visual Basic code, properties
- procedures [Visual Basic], calling
- properties [Visual Basic], property procedures
- procedure calls [Visual Basic], property procedures
ms.assetid: 96bc4d74-d9c3-4b7a-954d-58ac8553cd94
ms.openlocfilehash: 006961a0f1d4be6b0d52be5bc273dad9733bfe56
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388700"
---
# <a name="how-to-call-a-property-procedure-visual-basic"></a>方法: プロパティ プロシージャを呼び出す (Visual Basic)
プロパティ プロシージャを呼び出すには、プロパティに値を格納するか、その値を取得します。 プロパティには、変数にアクセスするのと同じ方法でアクセスします。  
  
 プロパティの `Set` プロシージャによって値が格納され、その `Get` プロシージャによって値が取得されます。 ただし、これらのプロシージャを名前で明示的に呼び出すことはしません。 変数の値を格納または取得する場合と同様に、代入ステートメントまたは式でもプロパティを使用します。 Visual Basic によってプロパティのプロシージャが呼び出されます。  
  
### <a name="to-call-a-propertys-get-procedure"></a>プロパティの Get プロシージャを呼び出すには  
  
1. 式内のプロパティ名は、変数名を使用する場合と同じように使用します。 変数または定数を使用できる場所であればどこでもプロパティを使用できます。  
  
     \- または -  
  
     代入ステートメント内で等号 (`=`) の後にプロパティ名を使用します。  
  
     次の例では、<xref:Microsoft.VisualBasic.DateAndTime.Now%2A> プロパティの値を読み取ることで、その `Get` プロシージャを暗黙的に呼び出します。  
  
     [!code-vb[VbVbalrDateProperties#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDateProperties/VB/Module1.vb#4)]  
  
2. プロパティが引数を受け取る場合は、プロパティ名の後にかっこで囲んだ引数リストを指定します。 引数がない場合は、必要に応じてかっこを省略できます。  
  
3. 引数リストの引数をコンマで区切ってかっこ内に配置します。 プロパティで定義されている対応するパラメーターと同じ順序で引数を指定してください。  
  
 プロパティの値は変数または定数の場合と同様に式に含められるか、または代入ステートメントの左辺にある変数またはプロパティに格納されます。  
  
### <a name="to-call-a-propertys-set-procedure"></a>プロパティの Set プロシージャを呼び出すには  
  
1. 代入ステートメントの左辺にプロパティ名を使用します。  
  
     次の例では、<xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A> プロパティの値を設定して、`Set` プロシージャを暗黙的に呼び出します。  
  
     [!code-vb[VbVbcnProcedures#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#11)]  
  
2. プロパティが引数を受け取る場合は、プロパティ名の後にかっこで囲んだ引数リストを指定します。 引数がない場合は、必要に応じてかっこを省略できます。  
  
3. 引数リストの引数をコンマで区切ってかっこ内に配置します。 プロパティで定義されている対応するパラメーターと同じ順序で引数を指定してください。  
  
 代入ステートメントの右辺で生成された値がプロパティに格納されます。  
  
## <a name="see-also"></a>関連項目

- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Property ステートメント](../../../language-reference/statements/property-statement.md)
- [Visual Basic のプロパティと変数の違い](./differences-between-properties-and-variables.md)
- [方法: プロパティを作成する](./how-to-create-a-property.md)
- [方法: 複数のアクセス レベルを持つプロパティを宣言する](./how-to-declare-a-property-with-mixed-access-levels.md)
- [方法: 既定のプロパティを宣言して呼び出す (Visual Basic)](./how-to-declare-and-call-a-default-property.md)
- [方法: プロパティに値を格納する](./how-to-put-a-value-in-a-property.md)
- [方法: プロパティから値を取得する](./how-to-get-a-value-from-a-property.md)
- [Get ステートメント](../../../language-reference/statements/get-statement.md)
- [Set ステートメント](../../../language-reference/statements/set-statement.md)
