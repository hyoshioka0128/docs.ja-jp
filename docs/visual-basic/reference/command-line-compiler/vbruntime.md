---
title: -vbruntime
ms.date: 03/13/2018
f1_keywords:
- vbruntime
- -vbruntime
helpviewer_keywords:
- vbruntime compiler option [Visual Basic]
- -vbruntime compiler option [Visual Basic]
- /vbruntime compiler option [Visual Basic]
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
ms.openlocfilehash: 31b719fb7e43cdd6ac44424b359999410dd608a5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403045"
---
# <a name="-vbruntime"></a>-vbruntime
コンパイラが Visual Basic Runtime Library を参照せずにコンパイルするか、特定のランタイム ライブラリを参照してコンパイルするかを指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-vbruntime:{ - | + | * | path }  
```  
  
## <a name="arguments"></a>引数  
 \-  
 Visual Basic ランタイム ライブラリを参照せずにコンパイルします。  
  
 \+  
 既定の Visual Basic ランタイム ライブラリを参照してコンパイルします。  
  
 \*  
 Visual Basic ランタイム ライブラリを参照せずにコンパイルし、Visual Basic ランタイム ライブラリからアセンブリにコア機能を埋め込みます。  
  
 `path`  
 指定したライブラリ (DLL) を参照してコンパイルします。  
  
## <a name="remarks"></a>Remarks  
 `-vbruntime` コンパイラ オプションでは、コンパイラで Visual Basic ランタイム ライブラリを参照せずにコンパイルするように指定することができます。 Visual Basic ランタイム ライブラリを参照せずにコンパイルする場合、エラーまたは警告は、Visual Basic ランタイム ヘルパーの呼び出しを生成するコードまたは言語コンストラクトに記録されます ("*Visual Basic ランタイム ヘルパー*" は、特定の言語のセマンティックを実行するために実行時に呼び出される、Microsoft.VisualBasic.dll 内に定義された関数です)。  
  
 `-vbruntime+` オプションでは、`-vbruntime` スイッチが指定されていない場合に発生する動作と同じ動作が生成されます。 `-vbruntime+` オプションを使用すると、それより前の `-vbruntime` スイッチをオーバーライドすることができます。  
  
 `-vbruntime-` または `-vbruntime:path` オプションを使用する場合、`My` 型のほとんどのオブジェクトは使用できません。  
  
## <a name="embedding-visual-basic-runtime-core-functionality"></a>Visual Basic ランタイム コア機能の埋め込み  
 `-vbruntime*` オプションを使用すると、ランタイム ライブラリを参照せずにコンパイルすることができます。 代わりに、Visual Basic ランタイム ライブラリのコア機能がユーザー アセンブリに埋め込まれます。 このオプションは、Visual Basic ランタイムを含まないプラットフォームでアプリケーションを実行する場合に使用することができます。  
  
 次のランタイム メンバーが埋め込まれます。  
  
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions> クラス  
  
- <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29> メソッド  
  
- <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29> メソッド  
  
- <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29> メソッド  
  
- <xref:Microsoft.VisualBasic.Constants.vbBack> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbCr> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbCrLf> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbFormFeed> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbLf> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbNewLine> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbNullChar> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbNullString> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbTab> 定数  
  
- <xref:Microsoft.VisualBasic.Constants.vbVerticalTab> 定数  
  
- `My` 型の一部のオブジェクト  
  
 `-vbruntime*` オプションを使用してコンパイルするときに、コア機能で埋め込まれない Visual Basic ランタイム ライブラリのメンバーをコードで参照している場合、そのメンバーが使用できないことを示すエラーがコンパイラから返されます。  
  
## <a name="referencing-a-specified-library"></a>指定したライブラリの参照  
 `path` 引数を使用すると、既定の Visual Basic ランタイム ライブラリの代わりに、カスタム ランタイム ライブラリを参照してコンパイルすることができます。  
  
 `path` 引数の値が DLL への完全修飾パスである場合、そのファイルがコンパイラでランタイム ライブラリとして使用されます。 `path` 引数の値が DLL への完全修飾パスではない場合、最初に現在のフォルダー内の指定した DLL が、Visual Basic コンパイラによって検索されます。 次に、[-sdkpath](sdkpath.md) コンパイラ オプションを使用して、指定したパスが検索されます。 `-sdkpath` コンパイラ オプションを使わない場合、指定した DLL がコンパイラによって、.NET Framework フォルダー (`%systemroot%\Microsoft.NET\Framework\versionNumber`) で検索されます。  
  
## <a name="example"></a>例  
 次の例は、`-vbruntime` オプションを使用して、カスタム ライブラリを参照してコンパイルする方法を示しています。  
  
```console
vbc -vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic コア - Visual Studio 2010 SP1 の新しいコンパイル モード](https://devblogs.microsoft.com/vbteam/vb-core-new-compilation-mode-in-visual-studio-2010-sp1/)
- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [-sdkpath](sdkpath.md)
