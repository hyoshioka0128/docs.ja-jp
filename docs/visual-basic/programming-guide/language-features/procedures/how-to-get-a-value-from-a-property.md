---
title: '方法: プロパティから値を取得する'
ms.date: 07/20/2015
helpviewer_keywords:
- property values [Visual Basic]
- Visual Basic code, procedures
- values [Visual Basic], properties
- Visual Basic code, properties
- properties [Visual Basic], values
ms.assetid: 3954423e-6ab7-4a4c-b55c-a8d27be47891
ms.openlocfilehash: 2c92cd4a869acbb7c8c52fbf4117112967386498
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387895"
---
# <a name="how-to-get-a-value-from-a-property-visual-basic"></a>方法: プロパティから値を取得する (Visual Basic)
プロパティの値を取得するには、プロパティ名を式に含めます。  
  
 プロパティの `Get` プロシージャによって値が取得されますが、名前で明示的に呼び出すことはありません。 変数を使用する場合と同様に、プロパティを使用します。 Visual Basic によってプロパティのプロシージャが呼び出されます。  
  
### <a name="to-retrieve-a-value-from-a-property"></a>プロパティから値を取得するには  
  
1. 式内のプロパティ名は、変数名を使用する場合と同じように使用します。 変数または定数を使用できる場所であればどこでもプロパティを使用できます。  
  
     \- または -  
  
     代入ステートメント内で等号 (`=`) の後にプロパティ名を使用します。  
  
     次の例では、Visual Basic `Now` プロパティの値を読み取り、その `Get` プロシージャを暗黙的に呼び出します。  
  
     [!code-vb[VbVbalrDateProperties#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDateProperties/VB/Module1.vb#4)]  
  
2. プロパティが引数を受け取る場合は、プロパティ名の後にかっこで囲んだ引数リストを指定します。 引数がない場合は、必要に応じてかっこを省略できます。  
  
3. 引数リストの引数をコンマで区切ってかっこ内に配置します。 プロパティで定義されている対応するパラメーターと同じ順序で引数を指定してください。  
  
 プロパティの値は変数または定数の場合と同様に式に含められるか、または代入ステートメントの左辺にある変数またはプロパティに格納されます。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Property ステートメント](../../../language-reference/statements/property-statement.md)
- [Visual Basic のプロパティと変数の違い](./differences-between-properties-and-variables.md)
- [方法: プロパティを作成する](./how-to-create-a-property.md)
- [方法: 複数のアクセス レベルを持つプロパティを宣言する](./how-to-declare-a-property-with-mixed-access-levels.md)
- [方法: プロパティ プロシージャを呼び出す](./how-to-call-a-property-procedure.md)
- [方法: 既定のプロパティを宣言して呼び出す (Visual Basic)](./how-to-declare-and-call-a-default-property.md)
- [方法: プロパティに値を格納する](./how-to-put-a-value-in-a-property.md)
