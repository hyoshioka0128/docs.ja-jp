---
title: XML ファイルの処理
ms.date: 07/20/2015
helpviewer_keywords:
- XML comments [Visual Basic], parsing [Visual Basic]
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
ms.openlocfilehash: 81d2c8d305e828b2963a0af9d97ec35b1745197a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398332"
---
# <a name="processing-the-xml-file-visual-basic"></a>XML ファイルの処理 (Visual Basic)
コンパイラは、ドキュメントを生成するためにタグ付けされたコードのコンストラクトごとに、ID 文字列を生成します。 (コードをタグ付けする方法については、[XML ドキュメント コメントのタグ](../../language-reference/xmldoc/index.md)に関する記事をご覧ください。)ID 文字列によって、コンストラクトは一意に識別されます。 XML ファイルを処理するプログラムでは、ID 文字列を使用して、対応する .NET Framework のメタデータまたはリフレクション項目を識別できます。  
  
 XML ファイルは、コードの階層表現ではなく、要素ごとに生成された ID を持つフラット リストです。  
  
 コンパイラは、次の規則に基づいて ID 文字列を生成します。  
  
- 文字列に空白は配置されません。  
  
- ID 文字列の最初の部分は、単一の文字とそれに続くコロンで識別されるメンバーの種類を示します。 次のメンバー型が使用されます。  
  
|文字|説明|  
|---|---|  
|N|namespace<br /><br /> ドキュメント コメントを名前空間に追加することはできませんが、名前空間への CREF 参照は作成できます (サポートされている場合)。|  
|T|型: `Class`、`Module`、`Interface`、`Structure`、`Enum`、`Delegate`|  
|F|フィールド: `Dim`|  
|P|プロパティ: `Property` (既定のプロパティを含む)|  
|M|メソッド: `Sub`、`Function`、`Declare`、`Operator`|  
|E|イベント: `Event`|  
|!|エラー文字列<br /><br /> あとに続く文字列で、エラーの情報を示します。 Visual Basic コンパイラは、解決できないリンクのエラー情報を生成します。|  
  
- `String` の 2 番目の部分は、名前空間のルートから始まる、項目の完全修飾名です。 項目の名前、それを囲む型、名前空間は、ピリオドで区切られます。 項目自体の名前にピリオドが含まれている場合、それらは番号記号 (#) に置き換えられます。 項目の名前に番号記号がないことが前提です。 たとえば、`String` コンストラクターの完全修飾名は `System.String.#ctor` になります。  
  
- プロパティおよびメソッドについては、メソッドに引数がある場合は、引数のリストをかっこで囲み、メソッドに続けて指定します。 引数がない場合は、かっこはありません。 引数はコンマで区切られます。 各引数のエンコードは、.NET Framework のシグネチャでのエンコード方法にそのまま従います。  
  
## <a name="example"></a>例  
 次のコードは、クラスとそのメンバーの ID 文字列を生成する方法を示しています。  
  
 [!code-vb[VbVbcnXmlDocComments#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#10)]  
  
## <a name="see-also"></a>関連項目

- [-doc](../../reference/command-line-compiler/doc.md)
- [方法: XML ドキュメントを作成する](how-to-create-xml-documentation.md)
