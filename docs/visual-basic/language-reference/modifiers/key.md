---
title: Key
ms.date: 07/20/2015
f1_keywords:
- vb.AnonymousKey
helpviewer_keywords:
- anonymous types [Visual Basic], key
- Key [Visual Basic]
- Key keyword [Visual Basic]
ms.assetid: 7697a928-7d14-4430-a72a-c9e96e8d6c11
ms.openlocfilehash: 5b060f5fa0042dfb8ffa6876f5e172d3bcda67a3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396221"
---
# <a name="key-visual-basic"></a>Key (Visual Basic)
`Key` キーワードを使用すると、匿名型のプロパティの動作を指定できます。 キー プロパティとして指定したプロパティのみが、匿名型インスタンス間の等価性のテスト、またはハッシュ コード値の計算に関与します。 キー プロパティの値は変更できません。  
  
 匿名型のプロパティをキー プロパティとして指定するには、初期化リストでその宣言の前にキーワード `Key` を配置します。 次の例では、`Airline` と `FlightNo` はキー プロパティですが、`Gate` は違います。  
  
 [!code-vb[VbVbalrAnonymousTypes#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#26)]  
  
 新しい匿名型を作成すると、<xref:System.Object> から直接継承されます。 コンパイラによって、継承された 3 つのメンバー (<xref:System.Object.Equals%2A>、<xref:System.Object.GetHashCode%2A>、および <xref:System.Object.ToString%2A>) がオーバーライドされます。 <xref:System.Object.Equals%2A> と <xref:System.Object.GetHashCode%2A> に対して生成されるオーバーライド コードは、キー プロパティに基づきます。 型にキー プロパティがない場合、<xref:System.Object.GetHashCode%2A> と <xref:System.Object.Equals%2A> はオーバーライドされません。  
  
## <a name="equality"></a>等価比較  
 2 つの匿名型のインスタンスは、それらが同じ型のインスタンスであり、それらのキー プロパティの値が等しい場合に等しいとされます。 次の例で、`flight2` は、前の例の `flight1` と等しくなります。それらは同じ匿名型のインスタンスであり、それらのキー プロパティで一致する値を持つためです。 ただし、`flight3` は、キー プロパティ `FlightNo` の値が異なるため、`flight1` と等しくありません。 インスタンス `flight4` は `flight1` と同じ型ではありません。それらはキー プロパティと異なるプロパティを指定しているためです。  
  
 [!code-vb[VbVbalrAnonymousTypes#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#27)]  
  
 2 つのインスタンスが、名前、型、順序、および値が同じで、非キー プロパティのみで宣言されている場合、2 つのインスタンスは等しくありません。 キー プロパティを持たないインスタンスは、それ自体とのみ等しくなります。  
  
 2 つの匿名型インスタンスが同じ匿名型のインスタンスである条件の詳細については、「[匿名型](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)」を参照してください。  
  
## <a name="hash-code-calculation"></a>ハッシュ コード計算  
 <xref:System.Object.Equals%2A> と同様に、匿名型の <xref:System.Object.GetHashCode%2A> に定義されているハッシュ関数は、型のキー プロパティに基づきます。 次の例に、キー プロパティとハッシュ コード値の間の相互作用を示します。  
  
 すべてのキー プロパティに同じ値を持つ匿名型のインスタンスは、同じハッシュ コード値を持ちます。非キー プロパティに一致する値がない場合でも同じです。 次のステートメントでは、`True` が返されます。  
  
 [!code-vb[VbVbalrAnonymousTypes#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#37)]  
  
 1 つ以上のキー プロパティで異なる値を持つ匿名型のインスタンスは、異なるハッシュ コード値を持ちます。 次のステートメントでは、`False` が返されます。  
  
 [!code-vb[VbVbalrAnonymousTypes#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#38)]  
  
 キー プロパティと異なるプロパティを指定する匿名型のインスタンスは、同じ型のインスタンスではありません。 それらは、すべてのプロパティの名前と値が同じであっても、異なるハッシュ コード値を持ちます。 次のステートメントでは、`False` が返されます。  
  
 [!code-vb[VbVbalrAnonymousTypes#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#39)]  
  
## <a name="read-only-values"></a>読み取り専用の値  
 キー プロパティの値は変更できません。 たとえば、前の例の `flight1` では、`Airline` フィールドと `FlightNo` フィールドは読み取り専用ですが、`Gate` は変更できます。  
  
 [!code-vb[VbVbalrAnonymousTypes#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#28)]  
  
## <a name="see-also"></a>関連項目

- [匿名型の定義](../../programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)
- [方法: 匿名型の宣言におけるプロパティ名と型を推論する](../../programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [匿名型](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)
