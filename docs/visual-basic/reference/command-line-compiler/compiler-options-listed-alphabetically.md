---
title: アルファベット順のコンパイラ オプション
ms.date: 04/12/2018
helpviewer_keywords:
- Visual Basic compiler, options
ms.assetid: e67febba-bacf-4e1f-a143-c141e063f90e
ms.openlocfilehash: 19e14953c08f90ea1ab245fa3124a462ccba162f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408739"
---
# <a name="visual-basic-compiler-options-listed-alphabetically"></a>Visual Basic コンパイラ オプション一覧 (アルファベット順)
Visual Basic コマンドライン コンパイラは、Visual Studio 統合開発環境 (IDE) からプログラムをコンパイルする方法の代替手段として提供されています。 次に、Visual Basic コマンドライン コンパイラ オプションの一覧 (アルファベット順) を示します。  

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]
  
|オプション|目的|  
|------------|-------------|  
|[@ (応答ファイルの指定)](specify-response-file.md)|応答ファイルを指定します。|  
|[-?](help.md)|コンパイラ オプションを出力します。 このコマンドは、`-help` オプションの指定と同じです。 コンパイルは発生しません。|  
|`-additionalfile`|コードの生成に直接影響はないが、エラーまたは警告を生成するためにアナライザーが使用できる追加のファイルを指定します。|  
|[-addmodule](addmodule.md)|指定ファイル内のすべての型情報を現在のコンパイル対象のプロジェクトで使用できるようにします。|  
|`-analyzer`|このアセンブリからアナライザーを実行します (短縮形: -a)。|  
|[-baseaddress](baseaddress.md)|DLL のベース アドレスを指定します。|  
|[-bugreport](bugreport.md)|バグを簡単に報告するための情報を含むファイルを作成します。|  
|`-checksumalgorithm:<alg>`|PDB に格納されているソース ファイルのチェックサムを計算するためのアルゴリズムを指定します。  サポートされる値は SHA1 (既定値) または SHA256 です。 <br>SHA1 には競合の問題があるため、Microsoft では SHA256 以上を推奨しています。|  
|[-codepage](codepage.md)|コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。|  
|[-debug](debug.md)|デバッグ情報を生成します。|  
|[-define](define.md)|条件付きコンパイルのシンボルを定義します。|  
|[-delaysign](delaysign.md)|アセンブリに完全に署名するか、部分的に署名するかを指定します。|  
|[-deterministic](deterministic.md)|入力が同一である場合、バイナリ コンテンツがコンパイル全体で同一のアセンブリをコンパイラに出力させます。|
|[-doc](doc.md)|ドキュメント コメントを XML ファイルに出力します。|  
|[-errorreport](errorreport.md)|Visual Basic コンパイラで内部コンパイル エラーを報告する方法を指定します。|  
|[-filealign](filealign.md)|出力ファイルでセクションをアラインするサイズを指定します。|  
|[-help](help.md)|コンパイラ オプションを出力します。 このコマンドは、`-?` オプションの指定と同じです。 コンパイルは発生しません。|  
|[-highentropyva](highentropyva.md)|特定の実行可能ファイルで高エントロピ ASLR (Address Space Layout Randomization) をサポートするかどうかを示します。|  
|[-imports](imports.md)|指定したアセンブリから名前空間をインポートします。|  
|[-keycontainer](keycontainer.md)|アセンブリに厳密な名前を付けるキー ペアのキー コンテナー名を指定します。|  
|[-keyfile](keyfile.md)|アセンブリに厳密な名前を付けるキーまたはキー ペアを含むファイルを指定します。|  
|[-langversion](langversion.md)|言語バージョンとして、9&#124;9.0&#124;10&#124;10.0&#124;11&#124;11.0 を指定します。|  
|[-libpath](libpath.md)|[-reference](reference.md) オプションにより参照されるアセンブリの場所を指定します。|  
|[-linkresource](linkresource.md)|マネージド リソースへのリンクを作成します。|  
|[-main](main.md)|起動時に使用する `Sub Main` プロシージャを含むクラスを指定します。|  
|[-moduleassemblyname](moduleassemblyname.md)|モジュールが一部となるアセンブリの名前を指定します。|  
|`-modulename:<string>`|ソース モジュールの名前を指定します。|  
|[-netcf](netcf.md)|.NET Compact Framework を対象とするようにコンパイラを設定します。|  
|[-noconfig](noconfig.md)|Vbc.rsp でコンパイルしないでください。|  
|[-nologo](nologo.md)|コンパイラの著作権情報が表示されないようにします。|  
|[-nostdlib](nostdlib.md)|コンパイラが標準ライブラリを参照しないようにします。|  
|[-nowarn](nowarn.md)|警告を生成するコンパイラの機能を無効にします。|  
|[-nowin32manifest](nowin32manifest.md)|アプリケーション マニフェストを実行可能ファイルに埋め込まないようコンパイラに指定します。|  
|[-optimize](optimize.md)|コードの最適化を有効または無効にします。|  
|[-optioncompare](optioncompare.md)|文字列比較をバイナリにするか、ロケール固有のテキストのセマンティクスを使用するかどうかを指定します。|  
|[-optionexplicit](optionexplicit.md)|変数の明示的な宣言を強制的に適用します。|  
|[-optioninfer](optioninfer.md)|変数宣言でローカル型推論を使用できるようにします。|  
|[-optionstrict](optionstrict.md)|厳密な言語セマンティクスを適用します。|  
|[-out](out.md)|出力ファイルを指定します。|  
|<code>-parallel[+&#124;-]</code>|同時実行ビルドを使用する (+) かどうかを指定します。|  
|[-platform](platform.md)|コンパイラによる出力ファイルの対象となるプロセッサ プラットフォームを指定します。|  
|`-preferreduilang`|出力用の言語名を指定します。|  
|[-quiet](quiet.md)|コンパイラで構文関連のエラーと警告のコードが表示されないようにします。|  
|[-recurse](recurse.md)|コンパイルするソース ファイルをサブディレクトリで検索します。|  
|[-reference](reference.md)|アセンブリからメタデータをインポートします。|  
|[/refonly](refonly-compiler-option.md)|参照アセンブリのみを出力します。|
|[/refout](refout-compiler-option.md)|参照アセンブリの出力パスを指定します。|
|[-removeintchecks](removeintchecks.md)|整数オーバーフローのチェックを無効にします。|  
|[-resource](resource.md)|マネージド リソースをアセンブリに埋め込みます。|  
|[-rootnamespace](rootnamespace.md)|すべての型宣言に対して名前空間を指定します。|  
|`-ruleset:<file>`|特定の診断を無効にするルールセット ファイルを指定します。|  
|[-sdkpath](sdkpath.md)|Mscorlib.dll および Microsoft.VisualBasic.dll の位置を指定します。|  
|[-subsystemversion](subsystemversion.md)|生成された実行可能ファイルが使用できるサブシステムの最低限のバージョンを指定します。|  
|[-target](target.md)|出力ファイルの形式を指定します。|  
|[-utf8output](utf8output.md)|UTF-8 エンコードを使用してコンパイラ出力を表示します。|  
|[-vbruntime](vbruntime.md)|コンパイラが Visual Basic Runtime Library を参照せずにコンパイルするか、特定のランタイム ライブラリを参照してコンパイルするかを指定します。|  
|[-verbose](verbose.md)|コンパイル中に追加の情報を出力します。|  
|[-warnaserror](warnaserror.md)|警告をエラーに昇格します。|  
|[-win32icon](win32icon.md)|.ico ファイルを出力ファイルに挿入します。|  
|[-win32manifest](win32manifest.md)|プロジェクトのポータブル実行可能 (PE) ファイルに埋め込まれる、ユーザー定義の Win32 アプリケーション マニフェスト ファイルを識別します。|  
|[-win32resource](win32resource.md)|Win32 リソースを出力ファイルに挿入します。|  
  
## <a name="see-also"></a>関連項目

- [Visual Basic コンパイラ オプション一覧 (カテゴリ別)](compiler-options-listed-by-category.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
