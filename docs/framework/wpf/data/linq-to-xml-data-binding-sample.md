---
title: LINQ to XML のデータ バインディングの例
ms.date: 10/22/2019
ms.topic: sample
helpviewer_keywords:
- linq to xml data binding sample
ms.openlocfilehash: aac814e4768a863a93e69e34cd18c941a9b35c89
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72921222"
---
# <a name="linq-to-xml-data-binding-sample"></a>LINQ to XML データ バインディングのサンプル

この記事では、ユーザー インターフェイス コンポーネントを埋め込み XML データ ソースにバインドする Windows Presentation Foundation (WPF) アプリである LinqToXmlDataBinding サンプルについて説明します。

## <a name="overview"></a>概要

LinqToXmlDataBinding サンプルは、C# と XAML のソース ファイルが含まれる Windows Presentation Foundation (WPF) アプリです。 埋め込み XML ドキュメントでは、書籍の一覧が定義されています。 ユーザーは、このアプリを使用して、書籍のエントリを表示、追加、削除、編集できます。

2 つの主要なソース ファイルがあります。

- [L2DBForm.xaml](l2dbform-xaml-source-code.md) には、メイン ウィンドウのユーザー インターフェイス (UI) の XAML 宣言コードが含まれています。 また、書籍一覧のデータ プロバイダーと埋め込み XML ドキュメントを定義するウィンドウ リソース セクションも含まれています。

- [L2DBForm.xaml.cs](l2dbform-xaml-cs-source-code.md) には、UI に関連付けられている初期化メソッドとイベント処理メソッドが含まれています。

メイン ウィンドウは縦に区切られ、次の 4 つの UI セクションに分かれています。

- **[XML]** には、組み込まれている書籍一覧の生の XML ソースが表示されます。

- **[Book List]** には書籍エントリが標準テキストで表示され、ユーザーはエントリを個別に選択および削除できます。

- **[Edit Selected Book]** では、ユーザーは現在選択している書籍エントリに関連付けられている値を編集できます。

- **[Add New Book]** では、ユーザーが入力した値に基づいて新しい書籍エントリを作成できます。

## <a name="run-the-sample"></a>サンプルを実行する

このセクションでは、Visual Studio で LinqToXmlDataBinding プロジェクトを作成してビルドする方法、および結果として生成される LinqToXmlDataBinding という Windows Presentation Foundation (WPF) アプリを実行する方法について説明します。

### <a name="create-the-project"></a>プロジェクトの作成

1. Visual Studio を開き、**LinqToXmlDataBinding** という名前の C# **WPF アプリ**を作成します。

   プロジェクトの対象は、.NET Framework 3.5 (またはそれ以降) にする必要があります。

1. 次の .NET アセンブリ用のプロジェクト参照がない場合は追加します。

    - System.Data
    - System.Data.DataSetExtensions
    - System.Xml
    - System.Xml

1. **Ctrl** キーと **Shift** キーを押しながら **B** キーを押してソリューションをビルドし、**F5** キーを押してそのソリューションを実行します。

   プロジェクトがエラーなくコンパイルされ、汎用 WPF アプリケーションとして実行されます。

### <a name="add-code"></a>コードの追加

1. **ソリューション エクスプローラー**でソース ファイルの名前を **Window1.xaml** から **L2XDBForm.xaml** に変更します。

   依存ソース ファイル Window1.xaml.cs の名前が、L2XDBForm.xaml.cs に自動的に変更されます。

1. ファイル **L2XDBForm.xaml** のソース コードを、[L2DBForm.xaml のソース コード](l2dbform-xaml-source-code.md)に置き換えます。 このファイルは XAML ソース ビューで操作します。

1. 同様に、**L2XDBForm.xaml.cs** のソースを、[L2DBForm.xaml.cs のソース コード](l2dbform-xaml-cs-source-code.md)に置き換えます。

1. ファイル **App.xaml** で、文字列 **Window1.xaml** をすべて **L2XDBForm.xaml** に置き換えます。

1. **Ctrl** キーと **Shift** キーを押しながら **B** キーを押して、ソリューションをビルドします。

### <a name="run-the-app"></a>アプリを実行する

LinqToXmlDataBinding プアプリを使用すると、ユーザーは、埋め込まれた XML 要素として格納されている書籍一覧を表示したり、操作したりできるようになります。 **F5** キー (デバッグ開始) または **Ctrl** + **F5** キー (デバッグなしで開始) を押して、アプリを実行します。

**[WPF Data Binding using LINQ to XML]** というタイトルのプログラム ウィンドウが表示されます。

UI の最上部に、書籍一覧を表す生の **XML** が表示されます。 この部分は WPF の <xref:System.Windows.Controls.TextBlock> コントロールを使って表示されており、マウスやキーボードで操作できません。

**[Book List]** というラベルの付いた 2 番目のセクションには、プレーンテキストの順序付けられた一覧として書籍が表示されます。 この部分では <xref:System.Windows.Controls.ListBox> コントロールが使用されており、マウスまたはキーボードによる選択が可能です。

### <a name="add-and-delete-books"></a>書籍を追加および削除する

一覧に新しい書籍を追加するには、最後のセクション **[Add New Book]** にある **[ID]** と **[Value]** の <xref:System.Windows.Controls.TextBox> コントロールに値を入力して、 **[Add Book]** を選択します。 書籍一覧と XML の両方に書籍が追加されます。 このプログラムでは入力値が検証されません。

一覧から既存の書籍を削除するには、 **[Book List]** セクションで書籍を選択し、 **[Remove Selected Book]** を選択します。 書籍一覧および生の XML ソースの両方で書籍のエントリが削除されます。

### <a name="edit-a-book-entry"></a>書籍のエントリを編集する

1. 2 番目の **[Book List]** セクションで書籍エントリを選択します。

   **[Edit Selected Book]** セクションにその現在の値が表示されます。

1. キーボードを使用して値を編集します。 いずれかの <xref:System.Windows.Controls.TextBox> コントロールがフォーカスを失った時点で、XML ソースと書籍一覧の両方に変更が自動的に反映されます。
