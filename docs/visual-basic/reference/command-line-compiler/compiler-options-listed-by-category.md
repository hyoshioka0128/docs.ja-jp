---
title: カテゴリ別のコンパイラ オプション
ms.date: 04/12/2018
helpviewer_keywords:
- Visual Basic compiler, options
ms.assetid: fbe36f7a-7cfa-4f77-a8d4-2be5958568e3
ms.openlocfilehash: 533d3da2f76854d311262ce97b43f240acab5f7d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408752"
---
# <a name="visual-basic-compiler-options-listed-by-category"></a>Visual Basic コンパイラ オプション一覧 (カテゴリ別)
Visual Basic コマンドライン コンパイラは、Visual Studio 統合開発環境 (IDE) 内からプログラムをコンパイルする方法の代替手段として提供されています。 機能のカテゴリ順に並べ替えた Visual Basic コマンド ライン コンパイラ オプションの一覧を次に示します。  

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]
  
## <a name="compiler-output"></a>コンパイラの出力  
  
|オプション|目的|  
|---|---|  
|[-nologo](nologo.md)|コンパイラの著作権情報が表示されないようにします。|  
|[-utf8output](utf8output.md)|UTF-8 エンコードを使用してコンパイラ出力を表示します。|  
|[-verbose](verbose.md)|コンパイル中に追加の情報を出力します。|  
|`-modulename:<string>`|ソース モジュールの名前を指定します。|  
|[/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|コンパイラ出力用の言語を指定します。|
  
## <a name="optimization"></a>最適化  
  
|オプション|目的|  
|---|---|  
|[-filealign](filealign.md)|出力ファイルでセクションをアラインするサイズを指定します。|  
|[-optimize](optimize.md)|最適化を有効または無効にします。|  
  
## <a name="output-files"></a>出力ファイル  
  
|オプション|目的|  
|---|---|  
|[-doc](doc.md)|ドキュメント コメントを XML ファイルに出力します。|  
|[-deterministic](deterministic.md)|入力が同一である場合、バイナリ コンテンツがコンパイル全体で同一のアセンブリをコンパイラに出力させます。|
|[-netcf](netcf.md)|.NET Compact Framework をターゲットとするようにコンパイラを設定します。|  
|[-out](out.md)|出力ファイルを指定します。|  
|[/refonly](refonly-compiler-option.md)|参照アセンブリのみを出力します。|
|[/refout](refout-compiler-option.md)|参照アセンブリの出力パスを指定します。|
|[-target](target.md)|出力の形式を指定します。|  
  
## <a name="net-assemblies"></a>.NET アセンブリ  
  
|オプション|目的|  
|---|---|  
|[-addmodule](addmodule.md)|指定ファイル内のすべての型情報を現在のコンパイル対象のプロジェクトで使用できるようにします。|  
|[-delaysign](delaysign.md)|アセンブリに完全に署名するか、部分的に署名するかを指定します。|  
|[-imports](imports.md)|指定したアセンブリから名前空間をインポートします。|  
|[-keycontainer](keycontainer.md)|アセンブリに厳密な名前を付けるキー ペアのキー コンテナー名を指定します。|  
|[-keyfile](keyfile.md)|アセンブリに厳密な名前を付けるキーまたはキー ペアを含むファイルを指定します。|  
|[-libpath](libpath.md)|[-reference](reference.md) オプションにより参照されるアセンブリの場所を指定します。|  
|[-reference](reference.md)|アセンブリからメタデータをインポートします。|  
|[-moduleassemblyname](moduleassemblyname.md)|モジュールが一部となるアセンブリの名前を指定します。|  
|`-analyzer`|このアセンブリからアナライザーを実行します (短縮形: -a)。|  
|`-additionalfile`|コードの生成に直接影響はないが、エラーまたは警告を生成するためにアナライザーが使用できる追加のファイルを指定します。|  
  
## <a name="debuggingerror-checking"></a>デバッグまたはエラー チェック  
  
|オプション|目的|  
|---|---|  
|[-bugreport](bugreport.md)|バグを簡単に報告するための情報を含むファイルを作成します。|  
|[-debug](debug.md)|デバッグ情報を生成します。|  
|[-nowarn](nowarn.md)|警告を生成するコンパイラの機能を無効にします。|  
|[-quiet](quiet.md)|コンパイラで構文関連のエラーと警告のコードが表示されないようにします。|  
|[-removeintchecks](removeintchecks.md)|整数オーバーフローのチェックを無効にします。|  
|[-warnaserror](warnaserror.md)|警告をエラーに昇格します。|  
|`-ruleset:<file>`|特定の診断を無効にするルールセット ファイルを指定します。|  
  
## <a name="help"></a>ヘルプ  
  
|オプション|目的|  
|---|---|  
|[-?](help.md)|コンパイラ オプションを出力します。 このコマンドは、`-help` オプションの指定と同じです。 コンパイルは発生しません。|  
|[-help](help.md)|コンパイラ オプションを出力します。 このコマンドは、`-?` オプションの指定と同じです。 コンパイルは発生しません。|  
  
## <a name="language"></a>言語  
  
|オプション|目的|  
|---|---|  
|[-langversion](langversion.md)|言語バージョンとして、9&#124;9.0&#124;10&#124;10.0&#124;11&#124;11.0.|  
|[-optionexplicit](optionexplicit.md)|変数の明示的な宣言を強制的に適用します。|  
|[-optionstrict](optionstrict.md)|厳密な型のセマンティクスを強制的に適用します。|  
|[-optioncompare](optioncompare.md)|文字列比較をバイナリにするか、ロケール固有のテキストのセマンティクスを使用するかどうかを指定します。|  
|[-optioninfer](optioninfer.md)|変数宣言でローカル型推論を使用できるようにします。|  
  
## <a name="preprocessor"></a>プリプロセッサ  
  
|オプション|目的|  
|---|---|  
|[-define](define.md)|条件付きコンパイルのシンボルを定義します。|  
  
## <a name="resources"></a>リソース  
  
|オプション|目的|  
|---|---|  
|[-linkresource](linkresource.md)|マネージド リソースへのリンクを作成します。|  
|[-resource](resource.md)|マネージド リソースをアセンブリに埋め込みます。|  
|[-win32icon](win32icon.md)|.ico ファイルを出力ファイルに挿入します。|  
|[-win32resource](win32resource.md)|Win32 リソースを出力ファイルに挿入します。|  
  
## <a name="miscellaneous"></a>その他  
  
|オプション|目的|  
|---|---|  
|[@ (応答ファイルの指定)](specify-response-file.md)|応答ファイルを指定します。|  
|[-baseaddress](baseaddress.md)|DLL のベース アドレスを指定します。|  
|[-codepage](codepage.md)|コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。|  
|[-errorreport](errorreport.md)|Visual Basic コンパイラで内部コンパイラ エラーを報告する方法を指定します。|  
|[-highentropyva](highentropyva.md)|特定の実行可能ファイルで高エントロピ ASLR (Address Space Layout Randomization) をサポートするかどうかを Windows カーネルに示します。|  
|[-main](main.md)|起動時に使用する `Sub Main` プロシージャを含むクラスを指定します。|  
|[-noconfig](noconfig.md)|コンパイルに Vbc.rsp が使用されないようにします。|  
|[-nostdlib](nostdlib.md)|コンパイラが標準ライブラリを参照しないようにします。|  
|[-nowin32manifest](nowin32manifest.md)|アプリケーション マニフェストを実行可能ファイルに埋め込まないようコンパイラに指定します。|  
|[-platform](platform.md)|コンパイラによる出力ファイルの対象となるプロセッサ プラットフォームを指定します。|  
|[-recurse](recurse.md)|コンパイルするソース ファイルをサブディレクトリで検索します。|  
|[-rootnamespace](rootnamespace.md)|すべての型宣言に対して名前空間を指定します。|  
|[-sdkpath](sdkpath.md)|Mscorlib.dll および Microsoft.VisualBasic.dll の位置を指定します。|  
|[-vbruntime](vbruntime.md)|コンパイラが Visual Basic Runtime Library を参照せずにコンパイルするか、特定のランタイム ライブラリを参照してコンパイルするかを指定します。|  
|[-win32manifest](win32manifest.md)|プロジェクトのポータブル実行可能 (PE) ファイルに埋め込まれる、ユーザー定義の Win32 アプリケーション マニフェスト ファイルを識別します。|  
|`-parallel[+&#124;-]`|同時実行ビルドを使用する (+) かどうかを指定します。|  
|`-checksumalgorithm:<alg>`|PDB に格納されているソース ファイルのチェックサムを計算するためのアルゴリズムを指定します。  サポートされる値は SHA1 (既定値) または SHA256 です。 <br>SHA1 には競合の問題があるため、Microsoft では SHA256 以上を推奨しています。|  
  
## <a name="see-also"></a>関連項目

- [Visual Basic コンパイラ オプション一覧 (アルファベット順)](compiler-options-listed-alphabetically.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
