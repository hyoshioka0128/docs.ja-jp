---
title: '方法: コマンド ライン コンパイラを起動する'
ms.date: 07/20/2015
helpviewer_keywords:
- command-line arguments
- vbc.exe
- Visual Basic compiler, starting
- command line [Visual Basic], arguments
ms.assetid: 0fd9a8f6-f34e-4c35-a49d-9b9bbd8da4a9
ms.openlocfilehash: 6def53d4a2d15dda3e3ac43abe35b3100f456fe9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408609"
---
# <a name="how-to-invoke-the-command-line-compiler-visual-basic"></a>方法: コマンド ライン コンパイラを起動する (Visual Basic)

コマンド ライン コンパイラを起動するには、実行可能ファイルの名前をコマンド ライン (MS-DOS プロンプトとも呼ばれます) に入力します。 既定の Windows コマンド プロンプトからコンパイルする場合は、実行可能ファイルへの完全修飾パスを入力する必要があります。 この既定の動作をオーバーライドするには、Visual Studio の開発者コマンド プロンプトを使用するか、または PATH 環境変数を変更します。 どちらの方法でも、コンパイラ名を入力するだけで、任意のディレクトリからコンパイルすることができます。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-invoke-the-compiler-using-the-developer-command-prompt-for-visual-studio"></a>Visual Studio の開発者コマンド プロンプトを使用してコンパイラを起動するには

1. Microsoft Visual Studio プログラム グループ内の Visual Studio Tools プログラム フォルダーを開きます。

2. Visual Studio がインストールされている場合は、Visual Studio の開発者コマンド プロンプトを使用して、ご使用のマシン上の任意のディレクトリからコンパイラにアクセスできます。

3. Visual Studio の開発者コマンド プロンプトを呼び出します。

4. コマンド ラインで「`vbc.exe` *sourceFileName*」と入力し、Enter キーを押します。

    たとえば、ソース コードを `SourceFiles` という名前のディレクトリに保存した場合は、コマンド プロンプトを開き「`cd SourceFiles`」と入力して、そのディレクトリに変更します。 ディレクトリに `Source.vb` という名前のソース ファイルが含まれている場合は、「`vbc.exe Source.vb`」と入力してコンパイルできます。

## <a name="to-set-the-path-environment-variable-to-the-compiler-for-the-windows-command-prompt"></a>Windows のコマンド プロンプト用のコンパイラに PATH 環境変数を設定するには

1. Windows 検索機能を使用して、ローカル ディスクで Vbc.exe を検索します。

    コンパイラが配置されているディレクトリの正確な名前は、Windows ディレクトリの場所とインストールされている ".NET Framework" のバージョンによって異なります。 ".NET Framework" の複数のバージョンがインストールされている場合は、使用するバージョン (通常は最新バージョン) を決定する必要があります。

2. **[スタート]** メニューから、 **[マイ コンピューター]** を右クリックし、ショートカット メニューから **[プロパティ]** をクリックします。

3. **[詳細設定]** タブをクリックし、 **[環境変数]** をクリックします。

4. **[システム変数]** ペインで、一覧から **[パス]** を選択し、 **[編集]** をクリックします。

5. **[システム変数の編集]** ダイアログ ボックスで、挿入ポイントを **[変数値]** フィールドの文字列の末尾に移動し、セミコロン (;) の後に手順 1 で見つかった完全なディレクトリ名を入力します。

6. **[OK]** をクリックして、編集内容を確認し、ダイアログ ボックスを閉じます。

     PATH 環境変数を変更すると、コンピューター上の任意のディレクトリから Windows コマンド プロンプトで Visual Basic コンパイラを実行できます。

## <a name="to-invoke-the-compiler-using-the-windows-command-prompt"></a>Windows のコマンド プロンプトを使用してコンパイラを起動するには

1. **[スタート]** メニューから、 **[アクセサリ]** フォルダーをクリックし、 **[Windows コマンドプロンプト]** を開きます。

2. コマンド ラインで「`vbc.exe`*sourceFileName*」と入力し、Enter キーを押します。

     たとえば、ソース コードを `SourceFiles` という名前のディレクトリに保存した場合は、コマンド プロンプトを開き「`cd SourceFiles`」と入力して、そのディレクトリに変更します。 ディレクトリに `Source.vb` という名前のソース ファイルが含まれている場合は、「`vbc.exe Source.vb`」と入力してコンパイルできます。

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md)
