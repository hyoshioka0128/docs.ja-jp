---
title: Option Explicit ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Explicit
- vb.OptionExplicit
helpviewer_keywords:
- declaring variables [Visual Basic], explicit
- forced variable declaration in Option Explicit statement [Visual Basic]
- Explicit keyword
- explicit variable declaration
- Option Explicit statement [Visual Basic]
ms.assetid: e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc
ms.openlocfilehash: a352df0323cfeca1ea0e206ae45c3f85a2cd7da3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404370"
---
# <a name="option-explicit-statement-visual-basic"></a>Option Explicit ステートメント (Visual Basic)
ファイル内のすべての変数の明示的な宣言を強制させるか、変数の暗黙的な宣言を許可します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Option Explicit { On | Off }  
```  
  
## <a name="parts"></a>指定項目  
 `On`  
 任意。 `Option Explicit` チェックを有効にします。 `On` または `Off` が指定されていない場合、既定値は `On` になります。  
  
 `Off`  
 任意。 `Option Explicit` チェックを無効にします。  
  
## <a name="remarks"></a>Remarks  
 `Option Explicit On` または `Option Explicit` がファイルに含まれている場合、`Dim` または `ReDim` ステートメントを使用して、すべての変数を明示的に宣言する必要があります。 宣言されていない変数名を使用しようとすると、コンパイル時にエラーが発生します。 `Option Explicit Off` ステートメントを使用すると、変数の暗黙的な宣言を許可します。  
  
 使用した場合、`Option Explicit` ステートメントはファイル内で他のソース コード ステートメントよりも前に記述する必要があります。  
  
> [!NOTE]
> `Option Explicit` を `Off` に設定することは、通常お勧めできません。 変数名のスペルを 1 か所以上間違えると、プログラムの実行時に予期しない結果を招く可能性があります。  
  
## <a name="when-an-option-explicit-statement-is-not-present"></a>Option Explicit ステートメントが指定されていない場合  
 ソース コードに `Option Explicit` ステートメントが含まれていない場合は、[[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) の **[Option Explicit]** 設定が使用されます。 コマンドライン コンパイラを使用している場合は、[-optionexplicit](../../reference/command-line-compiler/optionexplicit.md) コンパイラ オプションを使用します。  
  
#### <a name="to-set-option-explicit-in-the-ide"></a>IDE の Option Explicit を設定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[コンパイル]** タブをクリックします。  
  
3. **[Option Explicit]** ボックスに値を設定します。  
  
 新しいプロジェクトを作成すると、 **[コンパイル]** タブの **[Option Explicit]** 設定が **[VISUAL BASIC の既定値]** ダイアログ ボックスの **[Option Explicit]** 設定に設定されます。 **[VISUAL BASIC の既定値]** ダイアログ ボックスにアクセスするには、 **[ツール]** メニューで **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]** を展開し、 **[VISUAL BASIC の既定値]** をクリックします。 **[VISUAL BASIC の既定値]** の初期の既定値は `On` です。  
  
#### <a name="to-set-option-explicit-on-the-command-line"></a>コマンド ラインで Option Explicit を設定するには  
  
- **vbc** コマンドに [-optionexplicit](../../reference/command-line-compiler/optionexplicit.md) コンパイラ オプションを含めます。  
  
## <a name="example"></a>例  
 次の例では、`Option Explicit` ステートメントを使用して、すべての変数の明示的な宣言を強制しています。 宣言されていない変数を使用しようとすると、コンパイル時にエラーが発生します。  
  
 [!code-vb[VbVbalrStatements#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#47)]  
  
 [!code-vb[VbVbalrStatements#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#48)]  
  
## <a name="see-also"></a>関連項目

- [Dim ステートメント](dim-statement.md)
- [ReDim ステートメント](redim-statement.md)
- [Option Compare ステートメント](option-compare-statement.md)
- [Option Strict ステートメント](option-strict-statement.md)
- [-optioncompare](../../reference/command-line-compiler/optioncompare.md)
- [-optionexplicit](../../reference/command-line-compiler/optionexplicit.md)
- [-optionstrict](../../reference/command-line-compiler/optionstrict.md)
- [[Visual Basic の既定値] ([オプション] ダイアログ ボックス - [プロジェクト])](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
