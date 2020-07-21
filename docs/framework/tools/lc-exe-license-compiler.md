---
title: Lc.exe (ライセンス コンパイラ)
ms.date: 03/30/2017
helpviewer_keywords:
- Lc.exe
- .licx file
- License Compiler
- control licenses [Windows Forms]
- compiling licenses file
- license file
- .licenses file
- Windows Forms, control licenses
- licensed controls [Windows Forms]
ms.assetid: 2de803b8-495e-4982-b209-19a72aba0460
ms.openlocfilehash: 464514a241cc35fc821049ba0c29bec108d88253
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2020
ms.locfileid: "79180398"
---
# <a name="lcexe-license-compiler"></a>Lc.exe (ライセンス コンパイラ)
ライセンス コンパイラは、ライセンス情報を含むテキスト ファイルを読み込んで、バイナリ ファイルを生成します。このバイナリ ファイルは、リソースとして共通言語ランタイムの実行可能ファイルに埋め込むことができます。  
  
 .licx テキスト ファイルは、ライセンスされたコントロールがフォームに追加されると、Windows フォーム デザイナーによって自動的に生成または更新されます。 プロジェクト システムは、コンパイルの過程で、.licx テキスト ファイルを、.NET のコントロール ライセンス サポートを提供する .licenses バイナリのリソースに変換します。 バイナリのリソースは、その後、プロジェクト出力に埋め込まれます。  
  
 プロジェクトをビルドするときにライセンス コンパイラを使用した場合は、32 ビットと 64 ビットの間のクロス コンパイルはサポートされません。 これは、ライセンス コンパイラはアセンブリを読み込む必要があり、32 ビット アプリケーションからの 64 ビット アセンブリの読み込みおよびその逆は、許可されないためです。 この場合は、コマンド ラインからライセンス コンパイラを使用して手動でライセンスをコンパイルし、対応するアーキテクチャを指定します。  
  
 このツールは、Visual Studio と共に自動的にインストールされます。 このツールを実行するには、Visual Studio 用開発者コマンド プロンプト (または Windows 7 の Visual Studio コマンド プロンプト) を使用します。 詳細については、「[Visual Studio 用開発者コマンド プロンプト](developer-command-prompt-for-vs.md)」を参照してください。  
  
 コマンド プロンプトに次のように入力します。  
  
## <a name="syntax"></a>構文  
  
```console
      lc /target:  
targetPE /complist:filename [-outdir:path]  
/i:modules [/nologo] [/v]  
```  
  
|オプション|説明|  
|------------|-----------------|  
|**/complist:** *filename*|.licenses ファイルに組み込むライセンス付きコンポーネントの一覧を含むファイルの名前を指定します。 各コンポーネントを参照するにはフルネームを使用し、各行にコンポーネントを 1 つだけ指定します。<br /><br /> コマンド行を使用する場合は、プロジェクトに属するフォームごとに個別のファイルを指定できます。 Lc.exe は複数の入力ファイルを受け付けて、1 つの .licenses ファイルを生成します。|  
|**/h** **[elp]**|このツールのコマンド構文とオプションを表示します。|  
|**/i:** *module*|**/complist** ファイル内に一覧表示されたコンポーネントを含むモジュールを指定します。 複数のモジュールを指定するには、複数の **/i** フラグを使用します。|  
|**/nologo**|Microsoft 著作権情報を表示しません。|  
|**/outdir:** *path*|出力 .licenses ファイルを格納するディレクトリを指定します。|  
|**/target:** *targetPE*|.licenses ファイルを生成する実行可能ファイルを指定します。|  
|**/v**|詳細出力モードを指定します。コンパイルの進行状況に関する情報が表示されます。|  
|**@** *file*|応答 (.rsp) ファイルを指定します。|  
|**/?**|このツールのコマンド構文とオプションを表示します。|  
  
## <a name="example"></a>例  
  
1. `HostApp.exe` という名前のアプリケーション内の `Samples.DLL` に格納されているライセンス付きコントロール `MyCompany.Samples.LicControl1` を使用すると *、* 次の内容を含む `HostAppLic.txt` を作成できます。  
  
    ```text
    MyCompany.Samples.LicControl1, Samples.DLL  
    ```  
  
2. `HostApp.exe.licenses` という名前の .licenses ファイルを次のコマンドで作成します。  
  
    ```console  
    lc /target:HostApp.exe /complist:hostapplic.txt /i:Samples.DLL /outdir:c:\bindir  
    ```  
  
3. この .licenses ファイルをリソースとして含む  `HostApp.exe` を作成します。 C# アプリケーションを作成していた場合は、次のコマンドを使用してアプリケーションを作成します。  
  
    ```console
    csc /res:HostApp.exe.licenses /out:HostApp.exe *.cs  
    ```  
  
 `myApp.licenses`、`hostapplic.txt`、および `hostapplic2.txt` で指定されるライセンス付きコンポーネントの一覧から `hostapplic3.txt` をコンパイルするコマンドを次に示します。 引数 `modulesList` によって、ライセンス付きコンポーネントを含むモジュールを指定します。  
  
```console  
lc /target:myApp /complist:hostapplic.txt /complist:hostapplic2.txt /complist: hostapplic3.txt /i:modulesList  
```  
  
## <a name="response-file-example"></a>応答ファイルの例  
 次のリストは、`response.rsp` 応答ファイルの例を示しています。 応答ファイルの詳細については、「[応答ファイル](/visualstudio/msbuild/msbuild-response-files)」をご覧ください。  
  
```text  
/target:hostapp.exe  
/complist:hostapplic.txt
/i:WFCPrj.dll
/outdir:"C:\My Folder"  
```  
  
 次のコマンドラインで、この `response.rsp` ファイルを使用します。  
  
```console  
lc @response.rsp  
```  
  
## <a name="see-also"></a>関連項目

- [ツール](index.md)
- [Al.exe (アセンブリ リンカー)](al-exe-assembly-linker.md)
- [Visual Studio 用開発者コマンド プロンプト](developer-command-prompt-for-vs.md)
