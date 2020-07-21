---
title: Namespace ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Namespace
helpviewer_keywords:
- namespaces [Visual Basic], root
- Namespace statement [Visual Basic]
- namespaces [Visual Basic], nested
- declaring namespaces [Visual Basic], syntax
- namespaces [Visual Basic], declaring
- root namespaces
- declarations [Visual Basic], namespaces
ms.assetid: a31fbd95-9ace-4c3d-bbb1-51222a2272b2
ms.openlocfilehash: 0f1ba9a038fc604b6e4ede758891832e087fc096
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404435"
---
# <a name="namespace-statement"></a>Namespace ステートメント
名前空間の名前を宣言し、宣言に続くソース コードがその名前空間内でコンパイルされるようにします。  
  
## <a name="syntax"></a>構文  
  
```vb  
Namespace [Global.] { name | name.name }  
    [ componenttypes ]  
End Namespace  
```  
  
## <a name="parts"></a>指定項目  
 Global  
 任意。 これにより、プロジェクトのルート名前空間から名前空間を定義できます。 「[Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)」を参照してください。  
  
 `name`  
 必須です。 名前空間を識別する一意の名前。 有効な Visual Basic 識別子である必要があります。 詳細については、「[宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。  
  
 `componenttypes`  
 任意。 名前空間を構成する要素。 これには、列挙型、構造体、インターフェイス、クラス、モジュール、委任、その他の名前空間が含まれますが、この限りではありません。  
  
 `End Namespace`  
 `Namespace` ブロックを終了します。  
  
## <a name="remarks"></a>Remarks  
 名前空間は、組織的なシステムとして使用されます。 これを使用することにより、他のプログラムおよびアプリケーションに公開されるプログラミング要素を分類して提示することができます。 名前空間は、クラスまたは構造体がそうであるという意味では、"*型*" ではないことに注意してください。つまり、名前空間のデータ型を持つプログラミング要素を宣言することはできません。  
  
 `Namespace` ステートメントの後に宣言されるすべてのプログラミング要素は、その名前空間に属します。 Visual Basic は、`End Namespace` ステートメントまたは別の `Namespace` ステートメントのいずれかが検出されるまで、最後に宣言された名前空間に要素をコンパイルし続けます。  
  
 名前空間が既に定義されている場合 (ご使用のプロジェクト以外であっても)、プログラミング要素をそれに追加することができます。 このためには、`Namespace` ステートメントを使用して、要素をその名前空間にコンパイルするように Visual Basic に指示します。  
  
 `Namespace` ステートメントは、ファイルまたは名前空間レベルでのみ使用できます。 つまり、名前空間の "*宣言コンテキスト*" は、ソース ファイルまたは別の名前空間である必要があり、クラス、構造体、モジュール、インターフェイス、またはプロシージャにすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。  
  
 ある名前空間を別の名前空間内で宣言することができます。 宣言できる入れ子レベルに厳格な制限はありませんが、他のコードで、最も内側にある名前空間内で宣言された要素にアクセスする場合、入れ子階層内のすべての名前空間の名前を含む修飾文字列を使用する必要があることに注意してください。  
  
## <a name="access-level"></a>アクセス レベル  
 名前空間は、アクセス レベルが `Public` であるものとして扱われます。 名前空間は、同じプロジェクト内の任意の場所にあるコード、そのプロジェクトを参照する他のプロジェクト、そのプロジェクトから構築された任意のアセンブリからアクセスできます。  
  
 他の要素内部ではなく名前空間内という意味で、名前空間レベルで宣言されたプログラミング要素は、アクセス レベルを `Public` または `Friend` にすることができます。 指定しない場合、このような要素のアクセス レベルには、既定により、`Friend` が使用されます。 名前空間レベルで宣言できる要素としては、クラス、構造体、モジュール、インターフェイス、列挙型、委任があります。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。  
  
## <a name="root-namespace"></a>ルート名前空間  
 プロジェクト内のすべての名前空間の名前は、"*ルート名前空間*" に基づきます。 Visual Studio では、プロジェクト内のすべてのコードで、既定のルート名前空間としてプロジェクト名が割り当てられます。 たとえば、プロジェクト名が `Payroll`である場合、そのプログラミング要素は `Payroll`名前空間に属します。 `Namespace funding` を宣言する場合、その名前空間のフル ネームは `Payroll.funding` です。  
  
 ジェネリック リスト クラスの例のように、`Namespace` で既存の名前空間を指定する場合は、ルート名前空間を null 値に設定できます。 このためには、 **[プロジェクト]** メニューで **[プロジェクトのプロパティ]** をクリックし、 **[ルート名前空間]** エントリをクリアして、ボックスを空にします。 ジェネリック リスト クラスの例でこの操作を行わない場合、Visual Basic コンパイラは、`System.Collections.Generic` をプロジェクトの `Payroll` 内の新しい名前空間と見なし、フル ネームを `Payroll.System.Collections.Generic` にします。  
  
 または、`Global` キーワードを使用して、プロジェクトの外部で定義された名前空間の要素を参照することもできます。 こうすることにより、プロジェクト名をルート名前空間として保持できます。 これにより、プログラミング要素が既存の名前空間のプログラミング要素と誤ってマージされる可能性が低減されます。 詳細については、「[Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)」の「完全修飾名の Global キーワード」セクションを参照してください。  
  
 `Global` キーワードは、Namespace ステートメントでも使用できます。 これにより、プロジェクトのルート名前空間から名前空間を定義できます。 詳細については、「[Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)」の「名前空間のステートメントでの Global キーワード」セクションを参照してください。  
  
 **トラブルシューティング。** ルート名前空間によって、予期しない名前空間の名前の連結が生じる場合があります。 プロジェクトの外部で定義された名前空間を参照する場合、Visual Basic コンパイラは、それらをルート名前空間内の入れ子になった名前空間として解釈する可能性があります。 このような場合、コンパイラは、外部名前空間で既に定義されている型を認識しません。 これを回避するには、「ルート名前空間」で説明したようにルート名前空間を null 値に設定するか、`Global` キーワードを使用して外部名前空間の要素にアクセスします。  
  
## <a name="attributes-and-modifiers"></a>属性と修飾子  
 属性を名前空間に適用することはできません。 属性は、アセンブリのメタデータに情報を提供します。これは、名前空間などのソース分類子にとっては意味がありません。  
  
 アクセスまたはプロシージャ修飾子やその他の修飾子を名前空間に適用することはできません。 名前空間は型ではないため、これらの修飾子は意味がありません。  
  
## <a name="example"></a>例  
 次の例では、一方が他方の入れ子になる 2 つの名前空間を宣言します。  
  
 [!code-vb[VbVbalrStatements#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#43)]  
  
## <a name="example"></a>例  
 次の例では、入れ子になった複数の名前空間を 1 行で宣言します。これは、前の例と同じです。  
  
 [!code-vb[VbVbalrStatements#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#41)]  
  
## <a name="example"></a>例  
 次の例では、前の例で定義されたクラスにアクセスします。  
  
 [!code-vb[VbVbalrStatements#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#42)]  
  
## <a name="example"></a>例  
 次の例では、新しいジェネリック リスト クラスのスケルトンを定義し、それを <xref:System.Collections.Generic?displayProperty=nameWithType> 名前空間に追加します。  
  
```vb  
Namespace System.Collections.Generic  
    Class specialSortedList(Of T)  
        Inherits List(Of T)  
        ' Insert code to define the special generic list class.  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a>関連項目

- [Imports ステートメント (.NET 名前空間および型)](imports-statement-net-namespace-and-type.md)
- [宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)
- [Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)
