---
title: Get ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Get
helpviewer_keywords:
- Get statement [Visual Basic], syntax
- Get statement [Visual Basic]
- properties [Visual Basic], read-only
- read-only properties
- Get keyword [Visual Basic]
- property procedures [Visual Basic], Get statements
ms.assetid: 56b05cdc-bd64-4dfd-bb12-824eacec6f94
ms.openlocfilehash: 31936fb2c8f658203a43702a2b5fa4ee2481beb5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404603"
---
# <a name="get-statement"></a>Get ステートメント
プロパティの値を取得するために使用する `Get` プロパティ プロシージャを宣言します。  
  
## <a name="syntax"></a>構文  
  
```vb  
[ <attributelist> ] [ accessmodifier ] Get()  
    [ statements ]  
End Get  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`attributelist`|任意。 「[属性リスト](attribute-list.md)」を参照してください。|  
|`accessmodifier`|このプロパティの `Get` および `Set` ステートメントのいずれかで、省略可能です。 次のいずれかの値を指定します。<br /><br /> -   [Protected](../modifiers/protected.md)<br />-   [Friend](../modifiers/friend.md)<br />-   [Private](../modifiers/private.md)<br />-   `Protected Friend`<br /><br /> 「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。|  
|`statements`|任意。 `Get` プロパティ プロシージャが呼び出されたときに実行される 1 つ以上のステートメント。|  
|`End Get`|必須です。 `Get` プロパティ プロシージャの定義を終了します。|  
  
## <a name="remarks"></a>Remarks  
 プロパティが `WriteOnly` とマークされている場合を除き、すべてのプロパティには `Get` プロパティ プロシージャが必要です。 `Get` プロシージャは、プロパティの現在の値を返すために使用します。  
  
 Visual Basic では、式でプロパティの値が要求されると、プロパティの `Get` プロシージャが自動的に呼び出されます。  
  
 プロパティ宣言の本体には、[Property ステートメント](property-statement.md)と `End Property` ステートメントの間に、プロパティの `Get` と `Set` のプロシージャのみを含めることができます。 これらのプロシージャ以外のものを格納することはできません。 特に、プロパティの現在の値を格納することはできません。 この値は、プロパティの外部に格納する必要があります。それをいずれかのプロパティ プロシージャの内部に格納した場合、他のプロパティ プロシージャからアクセスできなくなるためです。 通常の方法は、プロパティと同じレベルで宣言された [Private](../modifiers/private.md) 変数に値を格納することです。 `Get` プロシージャは、適用先のプロパティの内部で定義する必要があります。  
  
 `Get` ステートメントで `accessmodifier` を使用しない限り、`Get` プロシージャは既定で、それを含んでいるプロパティのアクセス レベルに設定されます。  
  
## <a name="rules"></a>ルール  
  
- **混合アクセス レベル。** 読み取り/書き込みプロパティを定義する場合は、必要に応じて、`Get` または `Set` のいずれかのプロシージャに対して異なるアクセス レベルを指定できますが、両方に対して指定することはできません。 この場合、プロシージャのアクセス レベルは、プロパティのアクセス レベルよりも制限されている必要があります。 たとえば、プロパティが `Friend` として宣言されている場合は、`Get` プロシージャを、`Public` ではなく `Private` として宣言できます。  
  
     `ReadOnly` プロパティを定義する場合、`Get` プロシージャはプロパティ全体を表します。 `Get` に対して異なるアクセス レベルを宣言することはできません。それによって、プロパティに 2 つのアクセス レベルが設定されるためです。  
  
- **戻り値の型。** [Property ステートメント](property-statement.md)では、それによって返される値のデータ型を宣言できます。 `Get` プロシージャでは、そのデータ型が自動的に返されます。 任意のデータ型や、列挙、構造体、クラス、またはインターフェイスの名前を指定できます。  
  
     `Property` ステートメントで `returntype` を指定していない場合、プロシージャによって `Object` が返されます。  
  
## <a name="behavior"></a>動作  
  
- **プロシージャからの復帰。** `Get` プロシージャから呼び出し元のコードに戻ると、そのプロパティ値を要求したステートメント内で実行が続行されます。  
  
     `Get` プロパティ プロシージャでは、[Return ステートメント](return-statement.md)を使用するか、プロパティ名に戻り値を代入することによって、値を返すことができます。 詳細については、「[Function ステートメント](function-statement.md)」の "戻り値" に関する記述を参照してください。  
  
     `Exit Property` および `Return` ステートメントでは、プロパティ プロシージャがすぐに終了します。 任意の数の `Exit Property` および `Return` ステートメントをプロシージャ内の任意の場所に記述でき、`Exit Property` ステートメントと `Return` ステートメントを混在させることができます。  
  
- **戻り値。** `Get` プロシージャから値を返すには、プロパティ名に値を代入するか、[Return ステートメント](return-statement.md)に値を含めることができます。 `Return` ステートメントでは、`Get` プロシージャに戻り値を代入すると同時に、プロシージャが終了します。  
  
     プロパティ名に値を代入せずに、`Exit Property` を使用すると、`Get` プロシージャからは、プロパティのデータ型の既定値が返されます。 詳細については、「[Function ステートメント](function-statement.md)」の "戻り値" に関する記述を参照してください。  
  
     次の例では、読み取り専用プロパティ `quoteForTheDay` で、プライベート変数 `quoteValue` に保持されている値を返すことができる 2 つの方法を示しています。  
  
     [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]  
  
     [!code-vb[VbVbalrStatements#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#28)]  
  
     [!code-vb[VbVbalrStatements#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#29)]  
  
## <a name="example"></a>例  
 次の例では、`Get` ステートメントを使用してプロパティの値を返しています。  
  
 [!code-vb[VbVbalrStatements#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>関連項目

- [Set ステートメント](set-statement.md)
- [Property ステートメント](property-statement.md)
- [Exit ステートメント](exit-statement.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
- [チュートリアル: クラスの定義](../../programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)
