---
title: '方法: 既定のプロパティを宣言して呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- defaults [Visual Basic], properties
- properties [Visual Basic], default
- procedures [Visual Basic], defining
- default properties [Visual Basic], in Visual Basic
- Visual Basic code, procedures
- Visual Basic code, properties
- default properties
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
ms.openlocfilehash: 4de5d94a94e764d1fc543ffae41b00a9bb729c94
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388155"
---
# <a name="how-to-declare-and-call-a-default-property-in-visual-basic"></a>方法: Visual Basic で既定のプロパティを宣言して呼び出す
"*既定のプロパティ*" とは、コードで指定しなくてもアクセスできるクラスまたは構造体のプロパティです。 呼び出し元のコードでクラスまたは構造体の名前を指定し、プロパティ名を指定していないときに、コンテキストでプロパティへのアクセスが許可されている場合、Visual Basic はアクセスをそのクラスまたは構造体の既定のプロパティ (存在する場合) に解決します。  
  
 クラスまたは構造体は、最大 1 つの既定のプロパティを持つことができます。 ただし、既定のプロパティをオーバーロードし、複数のバージョンを用意することができます。  
  
 詳細については、「[Default](../../../language-reference/modifiers/default.md)」をご覧ください。  
  
### <a name="to-declare-a-default-property"></a>既定のプロパティを宣言するには  
  
1. 通常の方法でプロパティを宣言します。 `Shared` または `Private` キーワードは指定しないでください。  
  
2. プロパティ宣言に `Default` キーワードを含めます。  
  
3. プロパティに少なくとも 1 つのパラメーターを指定します。 1 つ以上の引数を受け取らない既定のプロパティを定義することはできません。  
  
     [!code-vb[VbVbcnProcedures#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#17)]  
  
### <a name="to-call-a-default-property"></a>既定のプロパティを呼び出すには  
  
1. 包含クラスまたは構造体の型の変数を宣言します。  
  
     [!code-vb[VbVbcnProcedures#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#16)]  
  
2. 通常はプロパティ名を含める式で変数名のみを使用します。  
  
     [!code-vb[VbVbcnProcedures#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#21)]  
  
3. 変数名の後に、かっこで囲んだ引数リストを指定します。 既定のプロパティは、少なくとも 1 つの引数を受け取る必要があります。  
  
     [!code-vb[VbVbcnProcedures#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#20)]  
  
4. 既定のプロパティ値を取得するには、式内または代入ステートメントの等号 (`=`) の後に、変数名と引数リストを使用します。  
  
     [!code-vb[VbVbcnProcedures#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#15)]  
  
5. 既定のプロパティ値を設定するには、代入ステートメントの左辺に変数名と引数リストを使用します。  
  
     [!code-vb[VbVbcnProcedures#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#14)]  
  
6. 他のプロパティにアクセスする場合と同様に、既定のプロパティ名は常に変数名と共に指定できます。  
  
     [!code-vb[VbVbcnProcedures#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#19)]  
  
## <a name="example"></a>例  
 次の例では、クラスの既定のプロパティを宣言しています。  
  
 [!code-vb[VbVbcnProcedures#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#12)]  
  
## <a name="example"></a>例  
 次の例は、`class1` クラスの既定のプロパティ `myProperty` を呼び出す方法を示しています。 3 つの代入ステートメントで `myProperty` に値を格納し、<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 呼び出しで値を読み取ります。  
  
 [!code-vb[VbVbcnProcedures#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#13)]  
  
 既定のプロパティの最も一般的な用途は、さまざまなコレクション クラスの <xref:Microsoft.VisualBasic.Collection.Item%2A> プロパティです。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 既定のプロパティを使用すると、ソース コード文字が少し少なくなる可能性がありますが、コードが読みにくくなる可能性があります。 呼び出し元のコードがクラスまたは構造体をよく理解していない場合は、クラスまたは構造体の名前を参照するときに、その参照がクラスまたは構造体自体、または既定のプロパティにアクセスするかどうかがわかりません。 これにより、コンパイラ エラーや実行時の微妙なロジック エラーが発生する可能性があります。  
  
 常に [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)を使用してコンパイラの型チェックを `On` に設定することにより、既定のプロパティ エラーが発生する可能性を多少減らすことができます。  
  
 定義済みのクラスまたは構造体をコード内で使用する予定の場合は、既定のプロパティがあるかどうかと、ある場合はその名前を確認する必要があります。  
  
 これらの欠点があるため、既定のプロパティを定義しないことを検討してください。 コードを読みやすくするためには、既定のプロパティを含め、常にすべてのプロパティを明示的に参照することも検討してください。  
  
## <a name="see-also"></a>関連項目

- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Property ステートメント](../../../language-reference/statements/property-statement.md)
- [default](../../../language-reference/modifiers/default.md)
- [Visual Basic のプロパティと変数の違い](./differences-between-properties-and-variables.md)
- [方法: プロパティを作成する](./how-to-create-a-property.md)
- [方法: 複数のアクセス レベルを持つプロパティを宣言する](./how-to-declare-a-property-with-mixed-access-levels.md)
- [方法: プロパティ プロシージャを呼び出す](./how-to-call-a-property-procedure.md)
- [方法: プロパティに値を格納する](./how-to-put-a-value-in-a-property.md)
- [方法: プロパティから値を取得する](./how-to-get-a-value-from-a-property.md)
