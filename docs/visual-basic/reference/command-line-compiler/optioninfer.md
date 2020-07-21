---
title: -optioninfer
ms.date: 07/20/2015
f1_keywords:
- -optioninfer
helpviewer_keywords:
- -optioninfer compiler option [Visual Basic]
- /optioninfer compiler option [Visual Basic]
- optioninfer compiler option [Visual Basic]
ms.assetid: f6c09db1-0553-464a-abe3-d4510c61d6ed
ms.openlocfilehash: 524660fca7c56fa490cc85169898bf2bf6d1a16e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400579"
---
# <a name="-optioninfer"></a>-optioninfer
変数宣言でローカル型推論を使用できるようにします。  
  
## <a name="syntax"></a>構文  
  
```console  
-optioninfer[+ | -]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`+` &#124; `-`|任意。 `-optioninfer+` を指定してローカル型推論を有効にするか、または `-optioninfer-` を指定してローカル型推論をブロックします。 `-optioninfer` オプションは、何も値を指定しない場合、`-optioninfer+` と同じです。 `-optioninfer` スイッチが存在しない場合の既定値も `-optioninfer+` です。 既定値は、Vbc.rsp 応答ファイル内に設定されています。|  
  
> [!NOTE]
> `-noconfig` オプションを使用すると、vbc.rsp に指定するのではなく、コンパイラの内部既定値を保持できます。 このオプションのコンパイラの既定値は `-optioninfer-` です。  
  
## <a name="remarks"></a>Remarks  
 ソース コード ファイルに [Option Infer](../../language-reference/statements/option-infer-statement.md) ステートメントが含まれている場合、そのステートメントによって `-optioninfer` コマンド ライン コンパイラ設定がオーバーライドされます。  
  
### <a name="to-set--optioninfer-in-the-visual-studio-ide"></a>Visual Studio IDE で -optioninfer を設定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[コンパイル]** タブで、 **[Option infer]** ボックスの値を変更します。  
  
## <a name="example"></a>例  
 次のコードは、ローカル型推論を有効にした状態で `test.vb` をコンパイルします。  
  
```console
vbc -optioninfer+ test.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-optioncompare](optioncompare.md)
- [-optionexplicit](optionexplicit.md)
- [-optionstrict](optionstrict.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [Option Infer ステートメント](../../language-reference/statements/option-infer-statement.md)
- [ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)
- [[Visual Basic の既定値] ([オプション] ダイアログ ボックス - [プロジェクト])](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
- [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [-noconfig](noconfig.md)
- [コマンド ラインからのビルド](building-from-the-command-line.md)
