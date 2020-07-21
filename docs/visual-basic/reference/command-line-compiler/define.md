---
title: -define
ms.date: 03/10/2018
helpviewer_keywords:
- -d compiler option [Visual Basic]
- /d compiler option [Visual Basic]
- -define compiler option [Visual Basic]
- d compiler option [Visual Basic]
- /define compiler option [Visual Basic]
- define compiler option [Visual Basic]
ms.assetid: f735c57d-1cf9-4f2f-a26f-0de630fd4077
ms.openlocfilehash: d0d1b03d9ab98f28a0112198f1ecc1e928d6d4a7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408713"
---
# <a name="-define-visual-basic"></a>-define (Visual Basic)
条件付きコンパイル定数を定義します。  
  
## <a name="syntax"></a>構文  
  
```console  
-define:["]symbol[=value][,symbol[=value]]["]  
```

or

```console  
-d:["]symbol[=value][,symbol[=value]]["]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`symbol`|必須です。 定義する記号。|  
|`value`|任意。 `symbol` に代入する値。 `value` が文字列の場合、引用符ではなく、バックスラッシュと引用符のシーケンス (\\") で囲む必要があります。 値が指定されていない場合は、True として処理されます。|  
  
## <a name="remarks"></a>Remarks  
 `-define` オプションは、ソース ファイル内で `#Const` プリプロセッサ ディレクティブを使用するのと同じ効果があります。ただし、`-define` を指定して定義する定数は public であり、プロジェクト内のすべてのファイルに適用されます。  
  
 このオプションで作成される記号を `#If`...`Then`...`#Else` ディレクティブで使用すると、ソース ファイルを条件付きでコンパイルできます。  
  
 `-d` は `-define` の省略形です。  
  
 記号の定義をコンマで区切ると、`-define` を使用して複数の記号を定義できます。  
  
|Visual Studio 統合開発環境で -define を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[コンパイル]** タブをクリックします。<br />3. **[詳細設定]** をクリックします。<br />4. **[カスタム定数]** ボックス内の値を変更します。|  
  
## <a name="example"></a>例  
 2 つの条件付きコンパイル定数を定義して使用する場合のコード例を次に示します。  
  
 [!code-vb[VbVbalrCompiler#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/Class1.vb#45)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [#If...Then...#Else ディレクティブ](../../language-reference/directives/if-then-else-directives.md)
- [#Const ディレクティブ](../../language-reference/directives/const-directive.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
