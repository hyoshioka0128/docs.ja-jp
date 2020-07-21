---
title: 構造化ナビゲーションの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- structured navigation [WPF]
ms.assetid: 025d30ef-fec5-436d-ad7a-5d5483331c26
ms.openlocfilehash: 5e8c27d017ed4bf8a7dcc2dda18877c9ed8dba69
ms.sourcegitcommit: 7bc6887ab658550baa78f1520ea735838249345e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75636342"
---
# <a name="structured-navigation-overview"></a>構造化ナビゲーションの概要

XAML ブラウザー アプリケーション (XBAP)、<xref:System.Windows.Controls.Frame>、または <xref:System.Windows.Navigation.NavigationWindow> でホストできるコンテンツは、パック Uniform Resource Identifier (URI) で識別され、ハイパーリンクで移動できるページで構成されています。 ページの構造、およびハイパーリンクで定義される移動方法を、ナビゲーション トポロジと呼びます。 このトポロジはさまざまな種類のアプリケーションに対応しますが、特にドキュメント間を移動するアプリケーションに適しています。 このようなアプリケーションでは、互いのページの情報を必要とせずに、ユーザーはページ間を移動できます。

ただし、アプリケーションによっては、移動のタイミングを理解している必要があるページを使用します。 たとえば、組織内のすべての従業員を一覧するページ ([従業員の一覧] ページ) を使用する人事アプリケーションがあるものとします。 このページでは、ハイパーリンクをクリックすることによって、新しい従業員を追加することもできます。 クリックすると、[従業員の追加] ページに移動して新しい従業員の詳細情報を収集します。次に、それを [従業員の一覧] ページに返して、新しい従業員を作成し、一覧を更新します。 このスタイルのナビゲーションは、構造化プログラミングと呼ばれる、処理を実行して値を返すメソッドの呼び出しに似ています。 そのため、このスタイルのナビゲーションを、*構造化ナビゲーション*と呼びます。

<xref:System.Windows.Controls.Page> クラスでは、構造化ナビゲーションのサポートは実装されていません。 代わりに、<xref:System.Windows.Navigation.PageFunction%601> クラスは <xref:System.Windows.Controls.Page> から派生し、構造化ナビゲーションに必要な基本コンストラクトで拡張されています。 このトピックでは、<xref:System.Windows.Navigation.PageFunction%601> を使用して構造化ナビゲーションを確立する方法について説明します。

<a name="Structured_Navigation"></a>

## <a name="structured-navigation"></a>構造化ナビゲーション

構造化ナビゲーションで、あるページが別のページを呼び出す場合、以下の一部またはすべての動作が必要です。

- 呼び出し元ページが、必要に応じてパラメーターを渡して、呼び出されたページに移動します。

- ユーザーが呼び出し元ページの使用を終了すると、呼び出されたページは呼び出し元ページに戻ります。このとき、次の動作が行われることがあります。

  - 呼び出し元ページの終了方法 (ユーザーが [OK] または [キャンセル] をクリックしたかどうかなど) を示す状態情報を返します。

  - ユーザーから収集したデータ (新しい従業員の詳細など) を返します。

- 呼び出し元ページが、呼び出されたページに戻ると、呼び出されたページはナビゲーション履歴から削除されて、呼び出されたページのインスタンスが他のインスタンスから分離されます。

これらの動作を次の図に示します。

![呼び出し元ページと呼び出し先ページの間のフローを示すスクリーンショット。](./media/structured-navigation-overview/flow-between-calling-page-called-page.png)

これらの動作は、呼び出し先ページとして <xref:System.Windows.Navigation.PageFunction%601> を使用することにより実装できます。

<a name="Structured_Navigation_with_PageFunction"></a>

## <a name="structured-navigation-with-pagefunction"></a>PageFunction を使用した構造化ナビゲーション

このトピックでは、単一の <xref:System.Windows.Navigation.PageFunction%601> を使用する構造化ナビゲーションの基本メカニズムを実装する方法について説明します。 このサンプルでは、<xref:System.Windows.Controls.Page> で <xref:System.Windows.Navigation.PageFunction%601> を呼び出して、ユーザーから <xref:System.String> 値を取得し、それを返します。

### <a name="creating-a-calling-page"></a>呼び出し元ページを作成する

<xref:System.Windows.Navigation.PageFunction%601> を呼び出すページには、<xref:System.Windows.Controls.Page> または <xref:System.Windows.Navigation.PageFunction%601> を使用できます。 次のコードに示すように、この例では <xref:System.Windows.Controls.Page> です。

[!code-xaml[StructuredNavigationSample#CallingPageDefaultMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#callingpagedefaultmarkup1)]
[!code-xaml[StructuredNavigationSample#CallingPageDefaultMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#callingpagedefaultmarkup2)]

[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind1)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind1)]
[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind2)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind2)]
[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND3](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind3)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind3)]

### <a name="creating-a-page-function-to-call"></a>呼び出すページ関数を作成する

呼び出し元ページは、呼び出されるページを使用してユーザーからデータを収集できるので、<xref:System.Windows.Navigation.PageFunction%601> は、呼び出されるページから返される値の型を型引数で指定するジェネリック クラスとして実装されます。 次のコードでは、<xref:System.Windows.Navigation.PageFunction%601> を使用して <xref:System.String> を返す、呼び出されるページの初期実装を示します。

[!code-xaml[StructuredNavigationSample#CalledPageFunctionMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml#calledpagefunctionmarkup)]

[!code-csharp[StructuredNavigationSample#CalledPageFunctionCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#calledpagefunctioncodebehind1)]
[!code-vb[StructuredNavigationSample#CalledPageFunctionCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#calledpagefunctioncodebehind1)]
[!code-csharp[StructuredNavigationSample#CalledPageFunctionCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#calledpagefunctioncodebehind2)]
[!code-vb[StructuredNavigationSample#CalledPageFunctionCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#calledpagefunctioncodebehind2)]

<xref:System.Windows.Navigation.PageFunction%601> の宣言は、型引数が追加された <xref:System.Windows.Controls.Page> の宣言に似ています。 コード例に示されているように、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップ (`x:TypeArguments` 属性を使用) と分離コード (標準のジェネリック型引数構文を使用) の両方で型引数が指定されています。

型引数として .NET Framework のクラスのみを使用する必要はありません。 <xref:System.Windows.Navigation.PageFunction%601> を呼び出して、カスタム型として抽象化されるドメイン固有のデータを収集できます。 <xref:System.Windows.Navigation.PageFunction%601> の型引数としてカスタム型を使用する方法を次のコードに示します。

[!code-csharp[CustomTypePageFunctionSnippets#CustomTypeCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomType.cs#customtypecode1)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypeCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomType.vb#customtypecode1)]
[!code-csharp[CustomTypePageFunctionSnippets#CustomTypeCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomType.cs#customtypecode2)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypeCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomType.vb#customtypecode2)]

[!code-xaml[CustomTypePageFunctionSnippets#CustomTypePageFunctionMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml#customtypepagefunctionmarkup1)]
[!code-xaml[CustomTypePageFunctionSnippets#CustomTypePageFunctionMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml#customtypepagefunctionmarkup2)]

[!code-csharp[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml.cs#customtypepagefunctioncodebehind1)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomTypePageFunction.xaml.vb#customtypepagefunctioncodebehind1)]
[!code-csharp[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml.cs#customtypepagefunctioncodebehind2)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomTypePageFunction.xaml.vb#customtypepagefunctioncodebehind2)]

<xref:System.Windows.Navigation.PageFunction%601> の型引数は、呼び出し元ページと呼び出されるページとの間の通信の基盤を提供します。この型引数については、次のセクションで説明します。

ここで示すように、<xref:System.Windows.Navigation.PageFunction%601> の宣言で示される型は、<xref:System.Windows.Navigation.PageFunction%601> から呼び出し元ページにデータを返すうえで重要な役割を果たします。

### <a name="calling-a-pagefunction-and-passing-parameters"></a>PageFunction を呼び出してパラメーターを渡す

ページを呼び出すには、呼び出し元ページで呼び出されるページをインスタンス化し、<xref:System.Windows.Navigation.NavigationService.Navigate%2A> メソッドを使用してそのページに移動する必要があります。 これにより、呼び出し元ページは、呼び出されるページで収集されるデータの既定値など、呼び出されるページに初期データを渡すことができます。

パラメーターなしではないコンストラクターを使用する呼び出されるページが、呼び出し元ページからパラメーターを受け取るコードを次に示します。

[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind1)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind1)]
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind2)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind2)]
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND3](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind3)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind3)]
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND4](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind4)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind4)]

呼び出し元ページで <xref:System.Windows.Documents.Hyperlink> の <xref:System.Windows.Documents.Hyperlink.Click> イベントを処理し、呼び出されるページをインスタンス化して、初期文字列値を渡すコードを次に示します。

[!code-xaml[StructuredNavigationSample#PassingDataMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#passingdatamarkup2)]
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind1)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind1)]
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind2)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind2)]
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND3](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind3)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind3)]

呼び出されるページにパラメーターを渡す必要はありません。 代わりに、以下を実行できます。

- 呼び出し元ページの場合:

  1. パラメーターなしコンストラクターを使用して、呼び出される <xref:System.Windows.Navigation.PageFunction%601> をインスタンス化します。

  2. <xref:System.Windows.Application.Properties%2A> にパラメーターを格納します。

  3. 呼び出される <xref:System.Windows.Navigation.PageFunction%601> に移動します。

- 呼び出される <xref:System.Windows.Navigation.PageFunction%601> の場合:

  - <xref:System.Windows.Application.Properties%2A> に格納されたパラメーターを取得および使用します。

しかし、この後の説明にもあるように、コードを使用して呼び出されたページをインスタンス化して、そのページに移動して、呼び出されたページから返されるデータを収集する必要が依然としてあります。 このため、<xref:System.Windows.Navigation.PageFunction%601> は有効である必要があります。有効でないと、次に <xref:System.Windows.Navigation.PageFunction%601> に移動したとき、WPF によりパラメーターなしのコンストラクターを使用して <xref:System.Windows.Navigation.PageFunction%601> がインスタンス化されます。

ただし、呼び出されたページが戻る前に、呼び出し元ページが取得できるデータを返す必要があります。

### <a name="returning-task-result-and-task-data-from-a-task-to-a-calling-page"></a>タスクから呼び出し元ページにタスク結果とタスク データを返す

ユーザーが呼び出されたページの使用を終了すると (この例では、[OK] または [キャンセル] をクリックすることで表されます)、呼び出されたページは戻る必要があります。 呼び出し元ページは、呼び出されたページを使用してユーザーからデータを収集したため、呼び出し元ページには 2 種類の情報が必要です。

1. ユーザーが呼び出されたページをキャンセルしたかどうか (この例では、[OK] と [キャンセル] のどちらをクリックしたかで表されます)。 これによって、呼び出し元ページは、ユーザーから収集したデータを処理するかどうかを判断します。

2. ユーザーが提供したデータ。

情報を返すには、<xref:System.Windows.Navigation.PageFunction%601> で <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> メソッドを実装します。 その呼び出し方法を次のコードに示します。

[!code-csharp[StructuredNavigationSample#ReturnCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#returncodebehind1)]
[!code-vb[StructuredNavigationSample#ReturnCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#returncodebehind1)]
[!code-csharp[StructuredNavigationSample#ReturnCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#returncodebehind2)]
[!code-vb[StructuredNavigationSample#ReturnCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#returncodebehind2)]

この例では、ユーザーが [キャンセル] をクリックすると、呼び出し元ページに値 `null` が返されます。 ユーザーが [OK] をクリックすると、ユーザーによって指定された文字列値が返されます。 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> は、データを呼び出し元ページに返すために呼び出す `protected virtual` メソッドです。 データは、ジェネリックな <xref:System.Windows.Navigation.ReturnEventArgs%601> 型のインスタンスにパッケージ化する必要があります。この型の型引数では、<xref:System.Windows.Navigation.ReturnEventArgs%601.Result%2A> が返す値の型を指定します。 このように、特定の型引数を使用して <xref:System.Windows.Navigation.PageFunction%601> を宣言することは、<xref:System.Windows.Navigation.PageFunction%601> が型引数で指定される型のインスタンスを返すことを示しています。 この例では、型引数、および戻り値が <xref:System.String> 型です。

<xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> を呼び出す場合、呼び出し元ページでは、<xref:System.Windows.Navigation.PageFunction%601> の戻り値を受け取るための方法が必要です。 そのため、<xref:System.Windows.Navigation.PageFunction%601> では、呼び出し元ページが処理する <xref:System.Windows.Navigation.PageFunction%601.Return> イベントが実装されています。 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> を呼び出すと、<xref:System.Windows.Navigation.PageFunction%601.Return> が発生するので、呼び出し元ページでは <xref:System.Windows.Navigation.PageFunction%601.Return> に登録して通知を受け取ることができます。

[!code-csharp[StructuredNavigationSample#ProcessResultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#processresultcodebehind1)]
[!code-vb[StructuredNavigationSample#ProcessResultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#processresultcodebehind1)]
[!code-csharp[StructuredNavigationSample#ProcessResultCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#processresultcodebehind2)]
[!code-vb[StructuredNavigationSample#ProcessResultCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#processresultcodebehind2)]

### <a name="removing-task-pages-when-a-task-completes"></a>タスク完了時にタスク ページを削除する

呼び出されたページが戻り、呼び出されたページをユーザーが取り消さなかった場合、呼び出し元ページでは、ユーザーから提供されたデータだけでなく、呼び出されたページから返されたデータも処理します。 このような方法で行われるデータ取得は、通常は分離されたアクティビティです。呼び出されたページが戻ると、呼び出し元ページでは、さらにデータをキャプチャするために、新しい呼び出し元ページを作成し、そこに移動する必要があります。

ただし、呼び出されたページが履歴から削除されない限り、ユーザーは呼び出し元ページの前のインスタンスに戻ることができます。 <xref:System.Windows.Navigation.PageFunction%601> が履歴に残っているかどうかは、<xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A> プロパティで判断されます。 既定では、<xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A> は `true` に設定されるため、ページ関数は <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> が呼び出されると自動的に削除されます。 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> が呼び出された後もページ関数をナビゲーション履歴内に残すには、<xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A> を `false` に設定します。

<a name="Other_Types_of_Structured_Navigation"></a>

## <a name="other-types-of-structured-navigation"></a>他の種類の構造化ナビゲーション

このトピックでは、構造化ナビゲーションの呼び出しと戻りをサポートする <xref:System.Windows.Navigation.PageFunction%601> の最も基本的な使用方法について説明します。 これに基づいて、より複雑な構造化ナビゲーションを作成できます。

たとえば、呼び出し元ページがユーザーから十分なデータを収集したり、タスクを実行するには、複数のページが必要な場合があります。 複数のページを使用する場合、これを "ウィザード" と呼びます。

また、構造化ナビゲーションに基づいて効率的な操作を実行する複雑なナビゲーション トポロジを使用するアプリケーションもあります。 詳細については、「[ナビゲーション トポロジの概要](navigation-topologies-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Navigation.PageFunction%601>
- <xref:System.Windows.Navigation.NavigationService>
- [ナビゲーション トポロジの概要](navigation-topologies-overview.md)
