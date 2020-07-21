---
title: ユーザー定義定数
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic], circular references
- Const statement [Visual Basic], user-defined constants
- user-defined constants [Visual Basic]
- scope [Visual Basic], constants
- constants [Visual Basic], user-defined
- circular references between constants [Visual Basic]
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
ms.openlocfilehash: 14f3de39eb8d8e6820e2b40792a8e8e57217e410
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414377"
---
# <a name="user-defined-constants-visual-basic"></a>ユーザー定義定数 (Visual Basic)
定数とは、不変の数値または文字列の代わりとなるわかりやすい名前です。 定数に格納された値は、その名が示すとおり、アプリケーションの実行中に変わることはありません。 処理するコントロールまたはコンポーネントで定義されている定数を使用するか、または独自に作成できます。 独自に作成した定数は、"*ユーザー定義*" と呼ばれます。  
  
 定数の宣言は、変数名を作成するときと同じガイドラインに従い、`Const` ステートメントを使用して行います。 `Option Strict` に `On` を指定した場合、定数の型を明示的に宣言する必要があります。  
  
## <a name="const-statement-usage"></a>Const ステートメントの使用法  
 `Const` ステートメントでは、数学的な数量または日時の値を表すことができます。  
  
 [!code-vb[VbEnumsTask#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#10)]  
  
 また、`String` 型の定数を定義することもできます。  
  
 [!code-vb[VbEnumsTask#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#13)]  
  
 通常、等号右側の式 ( `=` ) には数値またはリテラル文字列を指定しますが、数値または文字列が返される式を指定することもできます (ただし、式に関数の呼び出しは含められません)。 以前に定義した定数をもとに、定数を定義することもできます。  
  
 [!code-vb[VbEnumsTask#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#15)]  
  
## <a name="scope-of-user-defined-constants"></a>ユーザー定義定数のスコープ  
 `Const` ステートメントのスコープは、同じ場所で宣言されている変数と同じです。 次のいずれかの方法で、スコープを指定できます。  
  
- プロシージャ内にのみ存在する定数を作成するには、該当するプロシージャ内で宣言します。  
  
- クラス内のすべてのプロシージャで利用可能で、モジュール外のコードでは利用できない定数を作成するには、そのクラスの宣言セクションで宣言します。  
  
- アセンブリのすべてのメンバーで利用可能で、アセンブリのクライアント以外では利用できない定数を作成するには、クラスの宣言セクションで `Friend` キーワードを使用して宣言します。  
  
- アプリケーション全体で利用可能な定数を作成するには、クラスの宣言セクションで `Public` キーワードを使用して宣言します。  
  
 詳細については、[定数の宣言方法](how-to-declare-a-constant.md)に関するページを参照してください。  
  
### <a name="avoiding-circular-references"></a>循環参照の回避  
 定数は別の定数をもとに定義できるため、2 つ以上の定数間で "*サイクル*"、つまり循環参照を生み出してしまうことがあります。 循環参照は、次の例に示すように、パブリック定数が 2 つ以上あり、それぞれが他の定数をもとに定義されている場合に発生します。  
  
 [!code-vb[VbEnumsTask#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#16)]  
[!code-vb[VbEnumsTask#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#17)]  
  
 循環参照が発生すると、Visual Basic からコンパイラ エラーが生成されます。  
  
## <a name="see-also"></a>関連項目

- [Const ステートメント](../../../language-reference/statements/const-statement.md)
- [定数とリテラルのデータ型](constant-and-literal-data-types.md)
- [定数と列挙体](index.md)
- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
- [列挙型の概要](enumerations-overview.md)
- [定数の概要](constants-overview.md)
- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
