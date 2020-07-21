---
title: コード内の要素名としてのキーワード
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, naming conventions
- keywords [Visual Basic], in code
- name conflicts [Visual Basic]
- element names [Visual Basic], in code
ms.assetid: 2e4e8e02-23f7-49b9-a1c8-2b0402b6b525
ms.openlocfilehash: a98f0b027700717b414d58e1284ddec655eb25f7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403227"
---
# <a name="keywords-as-element-names-in-code-visual-basic"></a>コード内の要素名としてのキーワード (Visual Basic)
変数、クラス、メンバーなどのプログラム要素には、制限付きキーワードと同じ名前を付けることができます。 たとえば、`Loop` という名前の変数を作成できます。 ただし、制限付きキーワード `Loop` と同じ名前のバージョンを参照するには、次の例に示すように、名前の前に完全修飾文字列を指定するか、名前を角かっこ (`[ ]`) で囲む必要があります。  
  
 [!code-vb[VbVbcnConventions#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#8)]  
  
 次の例のように、これらのいずれも行わない場合、Visual Basic では組み込みキーワード `Loop` が使用されていると見なされ、エラーが生成されます。  
  
 `' The following statement causes a compiler error.`  
  
 `Loop.Visible = True`  
  
 フォームおよびコントロールを参照するときや、制限付きキーワードと同じ名前で変数を宣言したり、プロシージャを定義したりするときは、角かっこを使用できます。 名前を修飾したり、角かっこを含めたりするのを忘れやすいため、コードでエラーが発生し、読みにくくなります。 そのため、プログラム要素の名前として制限付きキーワードを使用しないことをお勧めします。 ただし、Visual Basic の将来のバージョンで、既存のフォームやコントロールの名前と競合する新しいキーワードが定義された場合は、その新しいバージョンで機能するようにコードを更新するときにこの手法を使用できます。  
  
> [!NOTE]
> また、他の参照アセンブリによって提供される要素名がプログラムに含まれている場合もあります。 これらの名前が制限付きキーワードと競合する場合は、それらを角かっこで囲むと、定義済みの要素と解釈されます。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の名前付け規則](naming-conventions.md)
- [プログラム構造とコード規則](program-structure-and-code-conventions.md)
- [キーワード](../../language-reference/keywords/index.md)
