---
title: '方法: 複数のアクセス レベルを持つプロパティを宣言する'
ms.date: 07/20/2015
helpviewer_keywords:
- access levels [Visual Basic], properties
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- mixed access levels
- Visual Basic code, properties
- properties [Visual Basic], access levels
- Property statement [Visual Basic], declaring mixed access levels
ms.assetid: fdbb2d97-279a-4956-b26c-cbdfbc34915a
ms.openlocfilehash: f0f7aba25888544dfcc093906850ae7ada621182
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388246"
---
# <a name="how-to-declare-a-property-with-mixed-access-levels-visual-basic"></a>方法: アクセス レベルの組み合わせを使用してプロパティを宣言する (Visual Basic)
プロパティに対する `Get` プロシージャと `Set` プロシージャに異なるアクセス レベルを設定する場合は、`Property` ステートメントで制限の少ないレベルを使用し、`Get` または `Set` ステートメントでより制限の厳しいレベルを使用できます。 コードの特定の部分でプロパティの値を取得できるようにし、コードの他の特定の部分で値を変更できるようにする場合は、そのプロパティに対してアクセス レベルの組み合わせを使用します。  
  
 アクセス レベルの詳細については、「[Access Levels in Visual Basic (Visual Basic でのアクセス レベル)](../declared-elements/access-levels.md)」をご覧ください。  
  
### <a name="to-declare-a-property-with-mixed-access-levels"></a>アクセス レベルの組み合わせを使用してプロパティを宣言するには  
  
1. 通常の方法でプロパティを宣言し、`Property` ステートメントで制限の少ないアクセス レベル (`Public` など) を指定します。  
  
2. より制限の厳しいアクセス レベル (`Friend` など) を指定して、`Get` または `Set` プロシージャを宣言します。  
  
3. もう一方のプロパティ プロシージャではアクセス レベルを指定しないでください。 `Property` ステートメントで宣言されたアクセス レベルが想定されています。 プロパティ プロシージャの 1 つでのみ、アクセスを制限できます。  
  
     [!code-vb[VbVbcnProcedures#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#10)]  
  
     上記の例では、`Get` プロシージャにはプロパティ自体と同じ `Protected` アクセスが設定され、`Set` プロシージャには `Private` アクセスが設定されます。 `employee` から派生したクラスは `salary` 値を読み取ることができますが、この値を設定できるのは `employee` クラスだけです。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Property ステートメント](../../../language-reference/statements/property-statement.md)
- [Visual Basic のプロパティと変数の違い](./differences-between-properties-and-variables.md)
- [方法: プロパティを作成する](./how-to-create-a-property.md)
- [方法: プロパティ プロシージャを呼び出す](./how-to-call-a-property-procedure.md)
- [方法: 既定のプロパティを宣言して呼び出す (Visual Basic)](./how-to-declare-and-call-a-default-property.md)
- [方法: プロパティに値を格納する](./how-to-put-a-value-in-a-property.md)
- [方法: プロパティから値を取得する](./how-to-get-a-value-from-a-property.md)
