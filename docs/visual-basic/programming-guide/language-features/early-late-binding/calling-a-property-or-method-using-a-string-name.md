---
title: 文字列名によるプロパティまたはメソッドの呼び出し
ms.date: 07/20/2015
helpviewer_keywords:
- passing operators [Visual Basic]
- strings [Visual Basic], passing new operators as
- objects [Visual Basic], setting properties
- setting properties, object properties at run time
- method calls [Visual Basic], strings
- methods [Visual Basic], calling with string names
- calling methods [Visual Basic], string names
- properties [Visual Basic], setting at run time
- CallByName function
ms.assetid: 79a7b8b4-b8c7-4ad8-aca8-12a9a2b32f03
ms.openlocfilehash: 29072479db36f9f8a81ffd7f3f5b10208ebaa984
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410658"
---
# <a name="calling-a-property-or-method-using-a-string-name-visual-basic"></a>文字列名によるプロパティまたはメソッドの呼び出し (Visual Basic)
オブジェクトのプロパティやメソッドは、デザイン時に把握して、これらを処理するコードを作成できることがほとんどです。 しかし、オブジェクトのプロパティやメソッドを事前に知ることができない場合や、実行時にエンド ユーザーがプロパティを指定したりメソッドを実行したりできる柔軟性を持たせたい場合があります。  
  
## <a name="callbyname-function"></a>CallByName 関数  
 例として、COM コンポーネントにユーザーが演算子を渡すことで入力した式を評価する、クライアント アプリケーションを考えます。 ここでは、新しい演算子が必要な新しい関数を、継続的にコンポーネントに追加するものとします。 標準的なオブジェクトへのアクセス手法を使用する場合、新しい演算子を使用するには、クライアント アプリケーションを再コンパイルして配布し直す必要があります。 これは、`CallByName` 関数を使用して新しい演算子を文字列として渡すことで回避できます。アプリケーションを変更する必要はありません。  
  
 `CallByName` 関数を使用すると、文字列を使用して実行時にプロパティまたはメソッドを指定することができます。 `CallByName` 関数のシグネチャは次のようになります。  
  
 *Result* = `CallByName`(<*オブジェクト*>, <*プロシージャ名*>, <*呼び出しの型*>, <*引数*>())  
  
 最初の引数である <*オブジェクト*> は、処理対象のオブジェクトの名前を取ります。 <*プロシージャ名*> 引数は、呼び出すメソッドまたはプロパティのプロシージャ名を含んだ文字列を取ります。 <*呼び出しの型*> 引数は、メソッド (`Microsoft.VisualBasic.CallType.Method`)、読み取り対象のプロパティ (`Microsoft.VisualBasic.CallType.Get`)、設定対象のプロパティ (`Microsoft.VisualBasic.CallType.Set`) のいずれかのうち、呼び出すプロシージャの型を表す定数を取ります。 <*引数*> 引数は省略可能であり、プロシージャに渡す引数が含まれる `Object` 型の配列を取ります。  
  
 `CallByName` は、現在のソリューションのクラスと共に使用できますが、多くの場合は、COM オブジェクトまたは .NET Framework アセンブリのオブジェクトにアクセスするために使用します。  
  
 次のコードに示すように、`SquareRoot` という名前の新しい関数を持つ、`MathClass` という名前のクラスが含まれるアセンブリへの参照を追加するとします。  
  
 [!code-vb[VbVbalrOOP#53](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#53)]  
  
 アプリケーションでテキスト ボックス コントロールを使用して、呼び出し対象のメソッドとその引数を制御できます。 たとえば、`TextBox1` に評価対象の式が含まれており、`TextBox2` を使用して関数名を入力する場合、次のコードを使用することで、`TextBox1` 内の式を対象とする `SquareRoot` 関数を呼び出すことができます。  
  
 [!code-vb[VbVbalrOOP#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#54)]  
  
 `TextBox1` に「64」、`TextBox2` に「SquareRoot」と入力してから `CallMath` プロシージャを呼び出すと、`TextBox1` に含まれる数字の平方根が算出されます。 この例のコードでは、`SquareRoot` 関数 (評価対象の式が含まれる文字列を必須引数として取ります) を呼び出して、`TextBox1` で "8" (64 の平方根) を返します。 当然のことながら、ユーザーが `TextBox2` に無効な文字列を入力するか、文字列にメソッド名ではなくプロパティ名が含まれているか、メソッドに追加の必須引数がある場合には、実行時エラーが発生します。 `CallByName` を使用するときには、こうしたエラーやその他のエラーも考慮して、堅牢なエラー処理コードを追加する必要があります。  
  
> [!NOTE]
> `CallByName` 関数は便利な場合もありますが、その有用性をパフォーマンスに対する影響と比較して考慮するようにしてください。`CallByName` を使用してプロシージャを呼び出すと、遅延バインディング呼び出しに比べてやや時間がかかります。 ループ内など、繰り返し呼び出される関数を呼び出す場合、`CallByName` を使用するとパフォーマンスに著しい負荷がかかる可能性があります。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Interaction.CallByName%2A>
- [オブジェクトの型の決定](determining-object-type.md)
