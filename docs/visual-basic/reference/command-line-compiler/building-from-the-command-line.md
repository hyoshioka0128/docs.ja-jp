---
title: コマンド ラインからのビルド
ms.date: 07/20/2015
helpviewer_keywords:
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers [Visual Basic], invoking from command line
- command-line builds
- compiling source code
- command-line compilers [Visual Basic], Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
ms.openlocfilehash: ec6ae3328c2042af950d1ee78a33d3de97219f10
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414299"
---
# <a name="building-from-the-command-line-visual-basic"></a>コマンド ラインからのビルド (Visual Basic)

Visual Basic プロジェクトは、1 つ以上の個別のソース ファイルで構成されます。 コンパイルと呼ばれるプロセス中に、これらのファイルが 1 つのパッケージ (アプリケーションとして実行できる 1 つの実行可能ファイル) にまとめられます。

Visual Basic では、Visual Studio 統合開発環境 (IDE) 内からプログラムをコンパイルするための代替手段として、コマンドライン コンパイラが提供されています。 コマンドライン コンパイラは、たとえば、システム メモリや記憶域スペースが制限されているコンピューターを使用したり、書き込みを行ったりする場合など、IDE のすべての機能を必要としない場合に適しています。

Visual Studio IDE 内からソース ファイルをコンパイルするには、 **[ビルド]** メニューから **[ビルド]** コマンドを選択します。

> [!TIP]
> Visual Studio IDE を使用してプロジェクト ファイルをビルドする場合、関連する **vbc** コマンドとそのスイッチに関する情報を出力ウィンドウに表示できます。 この情報を表示するには、[[オプション] ダイアログ ボックス、[プロジェクトおよびソリューション]、[ビルド/実行]](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run) の順に開き、 **[MSBuild プロジェクト ビルドの出力の詳細]** を **[通常]** またはそれ以上の詳細レベルに設定します。 詳細については、[ビルド ログ ファイルを表示、保存、および構成する](/visualstudio/ide/how-to-view-save-and-configure-build-log-files)」を参照してください。

MSBuild を使用して、コマンド プロンプトでプロジェクト (.vbproj) ファイルをコンパイルすることができます。 詳細については、「[コマンド ライン リファレンス](/visualstudio/msbuild/msbuild-command-line-reference)」と「[チュートリアル:MSBuild の使用](/visualstudio/msbuild/walkthrough-using-msbuild)に関するページを参照してください。

## <a name="in-this-section"></a>このセクションの内容

[方法: コマンド ライン コンパイラを起動する](how-to-invoke-the-command-line-compiler.md) \
MS-DOS プロンプトで、または特定のサブディレクトリからコマンドライン コンパイラを起動する方法について説明します。

[コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md) \
独自に使用するために変更できるサンプル コマンド ラインの一覧を示します。

## <a name="related-sections"></a>関連項目

[Visual Basic のコマンド ライン コンパイラ](index.md) \
アルファベット順または目的別に構成された、コンパイラ オプションの一覧を提供します。

[条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md) \
コードの特定のセクションをコンパイルする方法について説明します。

[Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio) \
さまざまなビルドに含まれる内容を整理し、プロジェクトのプロパティを選択し、プロジェクトが確実に正しい順序でビルドされるようにする方法について説明します。
