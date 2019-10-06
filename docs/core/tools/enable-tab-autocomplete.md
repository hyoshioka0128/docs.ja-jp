---
title: タブ補完を有効にする
description: この記事では、PowerShell、Bash、および zsh 向けの .NET Core CLI のタブ補完を有効にする方法を説明します。
author: thraka
ms.author: adegeo
ms.date: 12/17/2018
ms.openlocfilehash: 0f29ba2ef1d419339a0e2dc44f67c93b326eb40d
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182460"
---
# <a name="how-to-enable-tab-completion-for-net-core-cli"></a>.NET Core CLI のタブ補完を有効にする方法

.NET Core 2.0 SDK 以降では、.NET Core CLI はタブ補完をサポートします。 この記事では、3 つのシェル、PowerShell、Bash、および zsh のタブ補完を構成する方法について説明します。 その他のシェルでは、オート コンプリートのサポートがある場合があります。 オート コンプリートの構成方法については、それぞれのドキュメントを参照してください。手順は、この記事で説明されている手順と同様です。

[!INCLUDE [topic-appliesto-net-core-2plus](~/includes/topic-appliesto-net-core-2plus.md)]

セットアップが完了したら、シェルに `dotnet` コマンドを入力した後、TAB キーを押すと、.NET Core CLI のタブ補完がトリガーされます。 現在のコマンド ラインが `dotnet complete` コマンドに送信され、結果がシェルによって処理されます。 何かを `dotnet complete` コマンドに直接送信することで、タブ補完を有効にせずに結果をテストすることができます。 次に例を示します。

```console
> dotnet complete "dotnet a"
add
clean
--diagnostics
migrate
pack
```

そのコマンドが機能しない場合は、.NET Core 2.0 SDK 以降がインストールされていることを確認します。 インストールされているにもかかわらず、そのコマンドが機能しない場合は、`dotnet` コマンドが .NET Core 2.0 SDK 以降のバージョンに解決されることを確認します。 `dotnet --version` コマンドを使用して、現在のパスの解決先となっている `dotnet` のバージョンを確認します。 詳細については、「[使用する .NET Core のバージョンを選択する](../versions/selection.md)」を参照してください。

### <a name="examples"></a>使用例

タブ補完で提供されることの例をいくつか次に示します。

入力                                | 結果                                                                     | 理由
:------------------------------------|:----------------------------------------------------------------------------|:--------------------------------
`dotnet a⇥`                          | `dotnet add`                                                                 | アルファベット順では、`add` が最初のサブコマンドのため。
`dotnet add p⇥`                      | `dotnet add --help`                                                          | タブ補完が部分文字列と一致しており、アルファベット順では `--help` が先になるため。
`dotnet add p⇥⇥`                    | `dotnet add package`                                                          | Tab キーを 2 回押すと、次の修正候補が表示されるため。      
`dotnet add package Microsoft⇥`      | `dotnet add package Microsoft.ApplicationInsights.Web`                      | 結果はアルファベット順に返されるため。
`dotnet remove reference ⇥`          | `dotnet remove reference ..\..\src\OmniSharp.DotNet\OmniSharp.DotNet.csproj` | タブ補完がプロジェクト ファイルに対応しているため。

## <a name="powershell"></a>PowerShell

.NET Core CLI の **PowerShell** にタブ補完を追加するには、変数 `$PROFILE` に格納されているプロファイルを作成または編集します。 詳細については、[プロファイルの作成方法](/powershell/module/microsoft.powershell.core/about/about_profiles#how-to-create-a-profile)と[プロファイルと実行ポリシー](/powershell/module/microsoft.powershell.core/about/about_profiles#profiles-and-execution-policy)のトピックを参照してください。 

自分のプロファイルに次のコードを追加します。

```powershell
# PowerShell parameter completion shim for the dotnet CLI 
Register-ArgumentCompleter -Native -CommandName dotnet -ScriptBlock {
     param($commandName, $wordToComplete, $cursorPosition)
         dotnet complete --position $cursorPosition "$wordToComplete" | ForEach-Object {
            [System.Management.Automation.CompletionResult]::new($_, $_, 'ParameterValue', $_)
         }
 }
```

## <a name="bash"></a>Bash

.NET Core CLI の **bash** シェルにタブ補完を追加するには、次のコードを `.bashrc` ファイルに追加します。

```bash
# bash parameter completion for the dotnet CLI

_dotnet_bash_complete()
{
  local word=${COMP_WORDS[COMP_CWORD]}

  local completions
  completions="$(dotnet complete --position "${COMP_POINT}" "${COMP_LINE}")"

  COMPREPLY=( $(compgen -W "$completions" -- "$word") )
}

complete -f -F _dotnet_bash_complete dotnet
```

## <a name="zsh"></a>Zsh

.NET Core CLI の **zsh** シェルにタブ補完を追加するには、次のコードを `.zshrc` ファイルに追加します。

```zsh
# zsh parameter completion for the dotnet CLI

_dotnet_zsh_complete() 
{
  local completions=("$(dotnet complete "$words")")

  reply=( "${(ps:\n:)completions}" )
}

compctl -K _dotnet_zsh_complete dotnet
```
