---
title: -main
ms.date: 03/13/2018
helpviewer_keywords:
- main compiler option [Visual Basic]
- /main compiler option [Visual Basic]
- -main compiler option [Visual Basic]
ms.assetid: 83fc339d-6652-415d-b205-b5133319b5b0
ms.openlocfilehash: 5530da4c784346df4a1088998b8d2027feee08e3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403162"
---
# <a name="-main"></a>-main
`Sub Main` プロシージャを格納するクラスまたはモジュールを指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-main:location  
```  
  
## <a name="arguments"></a>引数  
 `location`  
 必須です。 プログラムの起動時に呼び出される `Sub Main` プロシージャを含むクラスまたはモジュールの名前。 この形式は、 **-main:module** または **-main:namespace.module** である場合があります。  
  
## <a name="remarks"></a>Remarks  
 このオプションは、実行可能ファイルまたは Windows 実行可能プログラムを作成するときに使用します。 **-main** オプションを省略した場合、すべてのパブリック クラスとモジュールから、有効な共有 `Sub Main` がコンパイラにより検索されます。  
  
 `Main` プロシージャのさまざまな形式については、「[Visual Basic の Main プロシージャ](../../programming-guide/program-structure/main-procedure.md)」を参照してください。  
  
 `location` が <xref:System.Windows.Forms.Form> から継承されるクラスである場合にクラスに `Main` プロシージャがないとき、アプリケーションを起動する既定の `Main` プロシージャがコンパイラによって提供されます。 これにより、開発環境で作成されたコードを、コマンド ラインでコンパイルできます。  
  
 [!code-vb[VbVbalrCompiler#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/Class1.vb#16)]  
  
### <a name="to-set--main-in-the-visual-studio-integrated-development-environment"></a>Visual Studio 統合開発環境で -main を設定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[アプリケーション]** タブをクリックします。  
  
3. **[アプリケーション フレームワークを有効にする]** チェック ボックスがオフになっていることを確認します。  
  
4. **[スタートアップ オブジェクト]** ボックスの値を変更します。  
  
## <a name="example"></a>例  
 次のコードでは、`Sub Main` プロシージャが `Test2` クラスにあることが指定され、`T2.vb` と `T3.vb` がコンパイルされます。  
  
```console
vbc t2.vb t3.vb -main:Test2  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-target (Visual Basic)](target.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [Visual Basic の Main プロシージャ](../../programming-guide/program-structure/main-procedure.md)
