---
title: Windows フォーム アプリケーションの基礎
ms.date: 07/20/2015
helpviewer_keywords:
- Windows applications
- Windows Forms, Visual Basic
ms.assetid: 0b919d30-7fd6-42db-85c8-543d15312441
ms.openlocfilehash: 11216186a28509e1f10bafa1b24a440bcedaeeb6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "85840383"
---
# <a name="windows-forms-application-basics-visual-basic"></a>Windows フォーム アプリケーションの基礎 (Visual Basic)

Visual Basic の重要な部分は、ユーザーのコンピューター上でローカルに実行される Windows フォーム アプリケーションを作成できることです。 Visual Studio を使用して、Windows フォームを使用したアプリケーションとユーザー インターフェイスを作成できます。 Windows フォーム アプリケーションは、<xref:System.Windows.Forms> 名前空間のクラスに基づいて構築されます。

## <a name="designing-windows-forms-applications"></a>Windows フォーム アプリケーションの設計

Visual Studio を使用して、Windows フォームおよび Windows サービス アプリケーションを作成できます。 詳細については、次のトピックを参照してください。

- 「[Windows フォームについて](../../../framework/winforms/getting-started-with-windows-forms.md)」。 Windows フォームを作成およびプログラミングする方法について説明します。

- 「[Windows フォーム コントロール](../../../framework/winforms/controls/index.md)」。 Windows フォーム コントロールの使用について説明しているトピックのコレクションです。

- [Windows サービス アプリケーション](../../../framework/windows-services/index.md)に関する記事。 Windows サービスの作成方法を説明するトピックの一覧を示しています。

## <a name="building-rich-interactive-user-interfaces"></a>リッチで対話型のユーザー インターフェイスの構築

Windows フォームは、.NET Framework のスマートクライアント コンポーネントであり、ファイル システムへの読み書きなど、アプリケーションの一般的なタスクを有効にするマネージド ライブラリのセットです。 Visual Studio などの開発環境を使用すると、情報を表示して、ユーザーからの入力を要求し、ネットワーク経由でリモート コンピューターと通信する Windows フォーム アプリケーションを作成できます。

Windows フォームでは、フォームはユーザーに情報を表示するビジュアル サーフェイスです。 通常は、コントロールをフォーム上に配置して、マウスのクリックやキーの押下などのユーザー アクションへの応答を開発することで、Windows フォーム アプリケーションを開発します。 "*コントロール*" は、データを表示したりデータ入力を受け入れたりする独立したユーザー インターフェイス (UI) 要素です。

### <a name="events"></a>イベント

ユーザーがフォームまたはそのコントロールのいずれかに何かを行うと、イベントが生成されます。 アプリケーションは、コードを使用してこれらのイベントに反応し、イベントが発生したときにそのイベントを処理します。 詳細については、「[Windows フォーム内でのイベント ハンドラーの作成](../../../framework/winforms/creating-event-handlers-in-windows-forms.md)」を参照してください。

### <a name="controls"></a>コントロール

Windows フォームには、テキスト ボックス、ボタン、ドロップダウン ボックス、ラジオ ボタン、そして Web ページなどを表示するコントロールなど、フォームに配置できるさまざまなコントロールが含まれています。 フォーム上で使用できるすべてのコントロールの一覧については、「[Windows フォームで使用するコントロール](../../../framework/winforms/controls/controls-to-use-on-windows-forms.md)」を参照してください。 既存のコントロールがニーズを満たしていない場合に、Windows フォームは <xref:System.Windows.Forms.UserControl> クラスを使用した独自のカスタム コントロールの作成もサポートしています。

Windows フォームには、Microsoft Office のようなハイエンド アプリケーションの機能をエミュレートする豊富な UI コントロールが用意されています。 <xref:System.Windows.Forms.ToolStrip> および <xref:System.Windows.Forms.MenuStrip> コントロールを使用すると、テキストとイメージを含むツールバーとメニューを作成したり、サブメニューを表示したり、テキスト ボックスやコンボ ボックスなど、その他のコントロールをホストしたりできます。

Visual Studio のドラッグアンドドロップ フォーム デザイナーを使用すると、Windows フォーム アプリケーションを簡単に作成できます。カーソルを使用してコントロールを選択し、フォーム上の任意の場所に配置するだけです。 デザイナーにはグリッド線や "スナップ線" などのツールが用意されているため、コントロールの調整が楽になります。 Visual Studio を使用する場合も、コマンド ラインでコンパイルする場合も、<xref:System.Windows.Forms.FlowLayoutPanel>、<xref:System.Windows.Forms.TableLayoutPanel>、および <xref:System.Windows.Forms.SplitContainer> コントロールを使用して、最小限の時間と労力で高度なフォーム レイアウトを作成できます。

### <a name="custom-ui-elements"></a>カスタム UI 要素

最後に、独自のカスタム UI 要素を作成する必要がある場合は、<xref:System.Drawing> 名前空間に、線、円、およびその他の図形をフォーム上に直接表示するために必要なすべてのクラスが含まれています。

これらの機能の使用に関する手順を追った説明については、次のヘルプ トピックを参照してください。

|終了|解決方法については、|
|--------|---------|
|Visual Studio を使用して新しい Windows フォーム アプリケーションを作成する|[チュートリアル 1: ピクチャ ビューアーの作成](/visualstudio/ide/tutorial-1-create-a-picture-viewer)|
|フォーム上のコントロールを使用する|[方法: Windows フォームにコントロールを追加する](../../../framework/winforms/controls/how-to-add-controls-to-windows-forms.md)|
|<xref:System.Drawing> を使用してグラフィックスを作成する|[グラフィックス プログラミングについて](../../../framework/winforms/advanced/getting-started-with-graphics-programming.md)|
|カスタム コントロールを作成する|[方法: UserControl クラスを継承する](../../../framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)|

## <a name="displaying-and-manipulating-data"></a>データの表示と操作

多くのアプリケーションは、データベース、XML ファイル、XML Web サービス、またはその他のデータ ソースからデータを表示する必要があります。 Windows フォームには、表形式データを従来の行と列の形式で表示するための、<xref:System.Windows.Forms.DataGridView> コントロールと呼ばれる柔軟なコントロールが用意されています。これにより、すべてのデータが独自のセルを占有するようになります。 <xref:System.Windows.Forms.DataGridView> を使用すると、個別のセルの外観のカスタマイズ、任意の列と行のその場でのロック、セルの内部の複雑なコントロールの表示や、その他の機能が可能になります。

ネットワーク経由のデータ ソースへの接続は、Windows フォームのスマート クライアントを使用すればシンプルなタスクです。 Visual Studio 2005 と .NET Framework 2.0 の Windows フォームで新しく導入された <xref:System.Windows.Forms.BindingSource> コンポーネントは、データ ソースへの接続を表すものであり、データをコントロールにバインドしたり、前のレコードと次のレコードに移動したり、レコードを編集したり、変更内容を元のソースに保存したりするためのメソッドが公開されます。 <xref:System.Windows.Forms.BindingNavigator> コントロールは、ユーザーがレコード間を移動する <xref:System.Windows.Forms.BindingSource> コンポーネントに対して、シンプルなインターフェイスを提供します。

### <a name="data-bound-controls"></a>データ バインド コントロール

[データソース] ウィンドウを使用すると、データ バインド コントロールを簡単に作成できます。このウィンドウには、プロジェクト内のデータベース、Web サービス、オブジェクトなどのデータ ソースが表示されます。 このウィンドウからプロジェクトのフォームに項目をドラッグして、データ バインド コントロールを作成できます。 また、[データ ソース] ウィンドウから既存のコントロールにオブジェクトをドラッグして、データに既存のコントロールをバインドすることもできます。

### <a name="settings"></a>設定

Windows フォームで管理できる別の種類のデータ バインディングは、設定です。 ほとんどのスマートクライアント アプリケーションでは、フォームの前回のサイズなどの実行時の状態に関する情報を一部保持し、保存されたファイルの既定の場所などのユーザー設定のデータを保持する必要があります。 アプリケーション設定機能は、クライアント コンピューターに両方の種類の設定を保存する簡単な方法を提供することで、こうした要件に対応します。 これらの定義は一度 Visual Studio またはコード エディターを使用して定義されると、XML として保持され、実行時に自動的にメモリに読み取られます。

これらの機能の使用に関する手順を追った説明については、次のヘルプ トピックを参照してください。

|終了|解決方法については、|
|--------|---------|
|<xref:System.Windows.Forms.BindingSource> コンポーネントを使用する|[方法: デザイナーを使用して Windows フォーム コントロールを BindingSource コンポーネントにバインドする](../../../framework/winforms/controls/bind-wf-controls-with-the-bindingsource.md)|
|ADO.NET データ ソースを操作する|[方法: Windows フォーム BindingSource コンポーネントで ADO.NET データを並べ替える/フィルター処理する](../../../framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|
|[データ ソース] ウィンドウを使用する|[チュートリアル: Windows フォームでのデータの表示](/visualstudio/data-tools/accessing-data-in-visual-studio)|

## <a name="deploying-applications-to-client-computers"></a>クライアント コンピューターにアプリケーションを配置する

アプリケーションを作成したら、それをユーザーに送信して、ユーザーが自分のクライアント コンピューターにインストールして実行できるようにする必要があります。 ClickOnce テクノロジを使用すると、数回クリックするだけで、Visual Studio の中からアプリケーションを配置して、Web 上のアプリケーションを指す URL をユーザーに提供することができます。 ClickOnce では、アプリケーションのすべての要素と依存関係が管理され、クライアント コンピューターにアプリケーションが正しくインストールされていることが確認されます。

ClickOnce アプリケーションは、ユーザーがネットワークに接続されている場合にのみ実行するか、またはオンラインとオフラインの両方で実行するかを構成することができます。 アプリケーションがオフライン操作をサポートするよう指定すると、ClickOnce によってユーザーの **[スタート]** メニューにアプリケーションへのリンクが追加されるため、ユーザーは URL を使用せずに開くことができるようになります。

アプリケーションを更新するときに、新しい配置マニフェストとアプリケーションの新しいコピーを Web サーバーに発行します。 ClickOnce によって、使用可能な更新プログラムがあることが検出され、ユーザーのインストールがアップグレードされます。古いアセンブリを更新するためのカスタム プログラミングは必要ありません。

ClickOnce の完全な概要については、「[ClickOnce のセキュリティと配置](/visualstudio/deployment/clickonce-security-and-deployment)」を参照してください。 これらの機能の使用に関する手順を追った説明については、次のヘルプ トピックを参照してください。

|終了|解決方法については、|
|--------|---------|
|ClickOnce を使用してアプリケーションを配置する|[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [チュートリアル: ClickOnce アプリケーションを手動で配置する](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|
|ClickOnce 配置を更新する|[方法: ClickOnce アプリケーションの更新プログラムを管理する](/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|
|ClickOnce を使用してセキュリティを管理する|[方法: [ClickOnce セキュリティ設定を有効にする]](/visualstudio/deployment/how-to-enable-clickonce-security-settings)|

## <a name="other-controls-and-features"></a>その他のコントロールおよび機能

Windows フォームには、ダイアログ ボックスの作成、ヘルプやドキュメントの印刷や追加、アプリケーションの複数言語へのローカライズのサポートなど、一般的なタスクを高速で簡単に実装できる機能が他にも多数あります。 さらに、Windows フォームは .NET Framework の堅牢なセキュリティ システムに依存しているため、より安全なアプリケーションを顧客にリリースできます。

これらの機能の使用に関する手順を追った説明については、次のヘルプ トピックを参照してください。

|終了|解決方法については、|
|--------|---------|
|フォームの内容を印刷する|[方法: Windows フォームでグラフィックスを印刷する](../../../framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [方法: Windows フォームで複数ページのテキスト ファイルを印刷する](../../../framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|
|Windows フォームのセキュリティについての詳細|[Windows フォームのセキュリティの概要](../../../framework/winforms/security-in-windows-forms-overview.md)|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- [Windows フォームの概要](../../../framework/winforms/windows-forms-overview.md)
- [My.Forms オブジェクト](../../language-reference/objects/my-forms-object.md)
