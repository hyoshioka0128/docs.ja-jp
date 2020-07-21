---
title: Visual Basic 言語のバージョンの選択
description: 特定のコンパイラ バージョンを使用して構文の検証を実行するように、コンパイラを構成します。
ms.date: 05/24/2018
ms.openlocfilehash: 4768d59a37d168b2883396f1dea4d0c1a0ff4ca7
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268269"
---
# <a name="select-the-visual-basic-language-version"></a>Visual Basic 言語のバージョンの選択

Visual Basic コンパイラは既定では、リリースされている言語の最新のメジャー バージョンに設定されています。 言語の新しいポイント リリースを使用して、プロジェクトをコンパイルすることができます。 言語の新しいバージョンを選択すると、プロジェクトで最新の言語機能を使用できます。 他のシナリオでは、古いバージョンの言語を使用する場合、プロジェクトがクリーンにコンパイルすることを検証する必要があります。

この機能によって、開発環境に新しいバージョンの SDK とツールをインストールすることの決定と新しい言語機能をプロジェクトに組み込むことの決定が別になります。 ビルド コンピューターに最新の SDK とツールをインストールできます。 特定バージョンの言語をビルドに使用するように各プロジェクトを構成できます。

言語バージョンを設定するには 3 つの方法があります。

- [ **.vbproj** ファイル](#edit-the-vbproj-file)を手動で編集する
- [サブディレクトリ内の複数のプロジェクトに対して](#configure-multiple-projects)言語バージョンを設定する
- [`-langversion` コンパイラ オプション](#set-the-langversion-compiler-option)を構成する

## <a name="edit-the-vbproj-file"></a>vbproj ファイルを編集する

**.vbproj** ファイルで言語バージョンを設定できます。 次の要素を追加します。

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

値 `latest` には、Visual Basic 言語の最新のマイナー バージョンを使用します。 次の値を指定できます。

|[値]|説明|
|------------|-------------|
|default|コンパイラは、最新のメジャー バージョンからサポートできるすべての有効な言語構文を受け入れます。|
|9|コンパイラは、Visual Basic 9.0 以前に含まれている構文のみを受け入れます。|
|10|コンパイラは、Visual Basic 10.0 以前に含まれている構文のみを受け入れます。|
|11|コンパイラは、Visual Basic 11.0 以前に含まれている構文のみを受け入れます。|
|12|コンパイラは、Visual Basic 12.0 以前に含まれている構文のみを受け入れます。|
|14|コンパイラは、Visual Basic 14.0 以前に含まれている構文のみを受け入れます。|
|15|コンパイラは、Visual Basic 15.0 以前に含まれている構文のみを受け入れます。|
|15.3|コンパイラは、Visual Basic 15.3 以前に含まれている構文のみを受け入れます。|
|15.5|コンパイラは、Visual Basic 15.5 以前に含まれている構文のみを受け入れます。|
|15.8|コンパイラは、Visual Basic 15.8 以前に含まれている構文のみを受け入れます。|
|latest|コンパイラは、サポートできるすべての有効な言語の構文を受け入れます。|

特殊文字列の `default` と `latest` はそれぞれ、ビルド コンピューターにインストールされている最新のメジャー言語バージョンとマイナー言語バージョンに解決されます。

## <a name="configure-multiple-projects"></a>複数のプロジェクトを構成する

複数のディレクトリを構成する `<LangVersion>` 要素を含む **Directory.build.props** ファイルを作成することができます。 この操作は通常、ソリューション ディレクトリで実行します。 ソリューション ディレクトリ内の **Directory.build.props** ファイルに以下を追加します。

```xml
<Project>
 <PropertyGroup>
   <LangVersion>15.5</LangVersion>
 </PropertyGroup>
</Project>
```

これで、そのファイルを含むディレクトリのすべてのサブディレクトリ内のビルドで、Visual Basic バージョン 15.5 構文が使用されます。 詳しくは、「[ビルドのカスタマイズ](/visualstudio/msbuild/customize-your-build)」を参照してください。

## <a name="set-the-langversion-compiler-option"></a>言語コンパイラ オプションを設定する

`-langversion` コマンド ライン オプションを使用することができます。 詳しくは、[-langversion](../reference/command-line-compiler/langversion.md) コンパイラ オプションに関する記事を参照してください。 「`vbc -langversion:?`」と入力して、有効な値の一覧を確認できます。
