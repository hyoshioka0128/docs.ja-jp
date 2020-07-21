---
title: '方法: プロパティを作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- Visual Basic code, properties
- properties [Visual Basic]
ms.assetid: 4d229712-6be8-4c5c-bac5-06995ce9185a
ms.openlocfilehash: fa220998d12206e620c242b9b39df3dc1b639d29
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388259"
---
# <a name="how-to-create-a-property-visual-basic"></a>方法: プロパティを作成する (Visual Basic)
プロパティ定義は、`Property` ステートメントと `End Property` ステートメントで囲みます。 この定義内で、`Get` プロシージャ、`Set` プロシージャ、またはその両方を定義します。 プロパティのすべてのコードは、これらのプロシージャ内にあります。  
  
 `Get` プロシージャ はプロパティの値を取得し、`Set` プロシージャは値を格納します。 プロパティに読み取り/書き込みアクセスが必要な場合は、両方のプロシージャを定義する必要があります。 読み取り専用プロパティでは `Get` のみを定義し、書き込み専用プロパティでは `Set` のみを定義します。  
  
### <a name="to-create-a-property"></a>プロパティを作成するには  
  
1. 任意のプロパティまたはプロシージャの外部で、[ Property ステートメント ](../../../language-reference/statements/property-statement.md) を使用し、その後に `End Property` ステートメントを使用します。  
  
2. プロパティがパラメーターを受け取る場合は、`Property` キーワードの後にプロシージャの名前を指定し、その後にかっこで囲んだパラメーター リストを指定します。  
  
3. かっこの後に `As` 句を入力して、プロパティの値のデータ型を指定します。 書き込み専用プロパティでもデータ型を指定する必要があります。  
  
4. 必要に応じて、`Get` および `Set` プロシージャを追加します。 以降の手順を参照してください。  
  
### <a name="to-create-a-get-procedure-that-retrieves-a-property-value"></a>プロパティ値を取得する Get プロシージャを作成するには  
  
1. `Property` ステートメントと `End Property` ステートメントの間に、[Get ステートメント](../../../language-reference/statements/get-statement.md)を記述し、その後に `End Get` ステートメントを記述します。 `Get` プロシージャのパラメーターを定義する必要はありません。  
  
2. `Get` ステートメントと `End Get` ステートメントの間に、プロパティの値を取得するコード ステートメントを配置します。 このコードでは、プロパティの値を生成して返すだけでなく、他の計算やデータ操作も含めることができます。  
  
3. `Return` ステートメントを使用して、プロパティの値を呼び出し元のコードに返します。  
  
 読み取り/書き込みプロパティと読み取り専用プロパティの `Get` プロシージャを記述する必要があります。 書き込み専用プロパティの `Get` プロシージャを定義することはできません。  
  
### <a name="to-create-a-set-procedure-that-writes-a-propertys-value"></a>プロパティの値を書き込む Set プロシージャを作成するには  
  
1. `Property` ステートメントと `End Property` ステートメントの間に、[Set ステートメント](../../../language-reference/statements/set-statement.md)を記述し、その後に `End Set` ステートメントを記述します。  
  
2. `Set` ステートメントで、`Set` キーワードの後に、かっこで囲まれたパラメーター リストを指定します。 このパラメーター リストには、呼び出し元のコードから渡される値の値パラメーターが少なくとも含まれている必要があります。 この値パラメーターの既定の名前は `Value` ですが、必要に応じて別の名前を使用できます。 値パラメーターは、プロパティ自体と同じデータ型である必要があります。  
  
3. `Set` ステートメントと `End Set` ステートメントの間に、プロパティに値を格納するコード ステートメントを配置します。 このコードでは、プロパティの値を検証して格納するだけでなく、他の計算やデータ操作も含めることができます。  
  
4. 値パラメーターを使用して、呼び出し元のコードで指定された値を受け入れます。 この値は、代入ステートメントで直接格納することも、式で使用して格納する内部値を計算することもできます。  
  
 読み取り/書き込みプロパティと書き込み専用プロパティの `Set` プロシージャを記述する必要があります。 読み取り専用プロパティの `Set` プロシージャを定義することはできません。  
  
## <a name="example"></a>例  
 次の例では、フル ネームを 2 つの構成要素名 (名と姓) として格納する読み取り/書き込みプロパティを作成します。 呼び出し元のコードが `fullName` を読み取ると、`Get` プロシージャが 2 つの構成要素名を結合し、フル ネームを返します。 呼び出し元のコードが新しいフル ネームを割り当てると、`Set` プロシージャがそれを 2 つの構成要素名に分割することを試みます。 スペースが見つからない場合は、すべてが名として格納されます。  
  
 [!code-vb[VbVbcnProcedures#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#8)]  
  
 次の例は、`fullName` のプロパティ プロシージャの一般的な呼び出しを示しています。 最初の呼び出しではプロパティ値を設定し、2 番目の呼び出しではそれを取得します。  
  
 [!code-vb[VbVbcnProcedures#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Visual Basic のプロパティと変数の違い](./differences-between-properties-and-variables.md)
- [方法: 複数のアクセス レベルを持つプロパティを宣言する](./how-to-declare-a-property-with-mixed-access-levels.md)
- [方法: プロパティ プロシージャを呼び出す](./how-to-call-a-property-procedure.md)
- [方法: 既定のプロパティを宣言して呼び出す (Visual Basic)](./how-to-declare-and-call-a-default-property.md)
- [方法: プロパティに値を格納する](./how-to-put-a-value-in-a-property.md)
- [方法: プロパティから値を取得する](./how-to-get-a-value-from-a-property.md)
