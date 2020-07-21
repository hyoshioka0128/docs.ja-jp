---
title: 条件付きコンパイル
ms.date: 07/20/2015
helpviewer_keywords:
- conditional compilation [Visual Basic], about conditional compilation
- compilation [Visual Basic], conditional
ms.assetid: 9c35e55e-7eee-44fb-a586-dad1f1884848
ms.openlocfilehash: c3eb1eb57b3d76e762ed53edb3b168ad96abec39
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403266"
---
# <a name="conditional-compilation-in-visual-basic"></a>Visual Basic での条件付きコンパイル
"*条件付きコンパイル*" では、プログラム内の特定のコード ブロックが選択的にコンパイルされ、他のコード ブロックは無視されます。  
  
 たとえば、同じプログラミング タスクに対するさまざまなアプローチの速度を比較するデバッグ ステートメントを記述したり、複数の言語用にアプリケーションをローカライズしたりできます。 条件付きコンパイル ステートメントは、実行時ではなく、コンパイル時に実行するように設計されています。  
  
 条件付きでコンパイルされるコード ブロックは、`#If...Then...#Else` ディレクティブで示します。 たとえば、同じソース コードから同じアプリケーションのフランス語バージョンとドイツ語バージョンを作成するには、事前定義された定数 `FrenchVersion` と `GermanVersion` を使用して、プラットフォーム固有のコード セグメントを `#If...Then` ステートメントに埋め込みます。 次の例はその方法を示しています。  
  
 [!code-vb[VbVbalrConditionalComp#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#5)]  
  
 コンパイル時に `FrenchVersion` 条件付きコンパイル定数の値を `True` に設定すると、フランス語バージョンの条件付きコードがコンパイルされます。 `GermanVersion` 定数の値を `True` に設定すると、コンパイラはドイツ語バージョンを使用します。 どちらも `True` に設定されていない場合は、最後の `Else` ブロックのコードが実行されます。  
  
> [!NOTE]
> コードが現在のブランチに含まれていない場合、コードを編集し、条件付きコンパイル ディレクティブを使用したときに、オートコンプリートは機能しません。  
  
## <a name="declaring-conditional-compilation-constants"></a>条件付きコンパイル定数の宣言  
 条件付きコンパイル定数は、次の 3 つの方法のいずれかで設定できます。  
  
- **プロジェクト デザイナー**内  
  
- コマンド ライン (コマンド ライン コンパイラを使用する場合)  
  
- コード内  
  
 条件付きコンパイル定数には特別なスコープがあり、標準コードからアクセスすることはできません。 条件付きコンパイル定数のスコープは、設定方法によって異なります。 次の表に、上記の 3 つの方法をそれぞれ使用して宣言された定数のスコープを示します。  
  
|定数の設定方法|定数のスコープ|  
|---|---|  
|**プロジェクト デザイナー**|プロジェクト内のすべてのファイルに対してパブリック|  
|コマンド ライン|コマンド ライン コンパイラに渡されるすべてのファイルに対してパブリック|  
|コード内の `#Const` ステートメント|これが宣言されているファイルに対してプライベート|  
  
|プロジェクト デザイナーで定数を設定するには|  
|---|  
|-   実行可能ファイルを作成する前に、「[プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)」に記載されている手順に従って、**プロジェクト デザイナー**で定数を設定します。|  
  
|コマンド ラインで定数を設定するには|  
|---|  
|-   次の例のように、 **-d** スイッチを使用して条件付きコンパイル定数を入力します。<br />     `vbc MyProj.vb /d:conFrenchVersion=–1:conANSI=0`<br />     **-d** スイッチと最初の定数の間にスペースは不要です。 詳細については、「[-define (Visual Basic)](../../reference/command-line-compiler/define.md)」をご覧ください。<br />     コマンド ラインの宣言は、**プロジェクト デザイナー**で入力された宣言をオーバーライドしますが、それらを消去するわけではありません。 **プロジェクト デザイナー**で設定した引数は、後続のコンパイルでも有効です。<br />     コード自体に定数を記述する場合、定数のスコープはそれらが宣言されているモジュール全体であるため、配置に関して厳密な規則はありません。|  
  
|コードで定数を設定するには|  
|---|  
|-   定数が使用されるモジュールの宣言ブロックに定数を配置します。 これにより、コードが整理され、読みやすくなります。|  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|---|---|  
|[プログラム構造とコード規則](program-structure-and-code-conventions.md)|コードを読みやすくし、管理しやすくするための推奨事項を示します。|  
  
## <a name="reference"></a>関連項目  
 [#Const ディレクティブ](../../language-reference/directives/const-directive.md)  
  
 [#If...Then...#Else ディレクティブ](../../language-reference/directives/if-then-else-directives.md)  
  
 [-define (Visual Basic)](../../reference/command-line-compiler/define.md)
