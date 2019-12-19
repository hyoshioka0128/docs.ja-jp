---
title: .NET Core 3.1 の新機能
description: .NET Core 3.1 の新機能について説明します。
dev_langs:
- csharp
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.openlocfilehash: 08ae824b79ba6a1ff5a92a0b4306eabe5ccadfd2
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74838309"
---
# <a name="whats-new-in-net-core-31"></a>.NET Core 3.1 の新機能

この記事では、.NET Core 3.1 の新機能について説明します。 このリリースには、小規模であるが重要な修正に重点を置いた .NET Core 3.0 のマイナー機能強化が含まれています。 .NET Core 3.1 に関する最も重要な機能は、[長期的なサポート (LTS)](#long-term-support) リリースであるということです。

Visual Studio 2019 を使用している場合は、.NET Core 3.1 プロジェクトを操作するために [Visual Studio 2019 16.4](https://visualstudio.microsoft.com/downloads/) に更新する必要があります。 Visual Studio 全体の新機能の詳細については、[Visual Studio のブログ](https://devblogs.microsoft.com/visualstudio/tis-the-season-visual-studio-2019/)を参照してください。

Visual Studio for Mac でも .NET Core 3.1 がサポートされており、Visual Studio for Mac 8.4 Preview チャネルに含まれています。 .NET Core 3.1 を使用するには、Preview チャネルを選択する必要があります。

リリースの詳細については、「[.NET Core 3.1 についてのお知らせ](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-1/)」を参照してください。

- Windows、macOS、または Linux 上に [.NET Core 3.1 をダウンロードして使い始めましょう](https://dotnet.microsoft.com/download/dotnet-core/3.1)。

## <a name="long-term-support"></a>長期サポート

.NET Core 3.1 は、次の 3 年間にわたって Microsoft のサポートが提供される LTS リリースです。 アプリを .NET Core 3.1 に移行することを強くお勧めします。 他のメジャー リリースの現在のライフサイクルは次のとおりです。

| 解放 | メモ |
| ------- | ---- |
| .NET Core 3.0 | 2020 年 3 月 3 日にサポートが終了します。     |
| .NET Core 2.2 | 2019 年 12 月 23 日にサポートが終了します。 |
| .NET Core 2.1 | 2021 年 8 月 21 日にサポートが終了します。    |

詳細については、「[.NET Core のサポート ポリシー](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)」をご覧ください。

## <a name="windows-forms"></a>Windows フォーム

*Windows のみ*

> [!WARNING]
> Windows フォームで破壊的変更が行われています。

Windows フォームには、Visual Studio Designer Toolbox でしばらくの間利用できなくなっているレガシ コントロールが含まれていました。 これらは、.NET Framework 2.0 の新しいコントロールに置き換えられていました。 これらは、Desktop SDK for .NET Core 3.1. から削除されています。

| 削除されたコントロール | 推奨代替 | 削除された関連 API |
| --------------- | ----------------------- | ----------------------- |
| DataGrid        | <xref:System.Windows.Forms.DataGridView>      | DataGridCell<br/>DataGridRow<br/>DataGridTableCollection<br/>DataGridColumnCollection<br/>DataGridTableStyle<br/>DataGridColumnStyle<br/>DataGridLineStyle<br/>DataGridParentRowsLabel<br/>DataGridParentRowsLabelStyle<br/>DataGridBoolColumn<br/>DataGridTextBox<br/>GridColumnStylesCollection<br/>GridTableStylesCollection<br/>HitTestType |
| ToolBar         | <xref:System.Windows.Forms.ToolStrip>         | ToolBarAppearance |
| ToolBarButton   | <xref:System.Windows.Forms.ToolStripButton>   | ToolBarButtonClickEventArgs<br/>ToolBarButtonClickEventHandler<br/>ToolBarButtonStyle<br/>ToolBarTextAlign |
| ContextMenu     | <xref:System.Windows.Forms.ContextMenuStrip>  |  |
| :::no-loc text="Menu"::: | <xref:System.Windows.Forms.ToolStripDropDown><br/><xref:System.Windows.Forms.ToolStripDropDownMenu> | MenuItemCollection |
| MainMenu        | <xref:System.Windows.Forms.MenuStrip>         |  |
| MenuItem        | <xref:System.Windows.Forms.ToolStripMenuItem> |  |

アプリケーションを .NET Core 3.1 に更新し、コントロールの置き換えを行うことをお勧めします。 コントロールの置き換えは、基本的には型の "検索と置換" という単純なプロセスです。

## <a name="ccli"></a>C++/CLI

*Windows のみ*

C++/CLI (別名 "マネージド C++") プロジェクトを作成するためのサポートが追加されています。 これらのプロジェクトから生成されるバイナリは、.NET Core 3.0 以降のバージョンと互換性があります。

Visual Studio 2019 16.4 に C++/CLI のサポートを追加するには、[C++ ワークロードを使用するデスクトップ開発](https://docs.microsoft.com/cpp/build/vscpp-step-0-installation?view=vs-2019#step-4---choose-workloads)をインストールします。 このワークロードによって、次の 2 つのテンプレートが Visual Studio に追加されます。

- CLR クラス ライブラリ (.NET Core)
- CLR 空のプロジェクト (.NET Framework)

## <a name="next-steps"></a>次の手順

- [.NET Core 3.0 と 3.1 の間の破壊的変更を確認する](../compatibility/3.0-3.1.md)
- [Windows フォーム アプリ用の .NET Framework と .NET Core 3.0 の間の破壊的変更を確認します。](../porting/winforms-breaking-changes.md)
