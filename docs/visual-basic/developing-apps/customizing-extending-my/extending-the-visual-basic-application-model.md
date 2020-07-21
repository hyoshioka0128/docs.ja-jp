---
title: Visual Basic アプリケーション モデルの拡張
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic Application Model, extending
ms.assetid: e91d3bed-4c27-40e3-871d-2be17467c72c
ms.openlocfilehash: e707f034f05aababdc70d5d6e1f9e1da0ed558bc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410232"
---
# <a name="extending-the-visual-basic-application-model"></a>Visual Basic アプリケーション モデルの拡張

アプリケーション モデルに機能を追加するには、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> クラスの `Overridable` メンバーをオーバーライドします。 この手法を使用して、アプリケーション モデルの動作をカスタマイズし、アプリケーションの起動時およびシャットダウン時に、独自のメソッドの呼び出しを追加できます。

## <a name="visual-overview-of-the-application-model"></a>アプリケーション モデルの視覚的な概要

このセクションでは、Visual Basic アプリケーション モデルでの関数呼び出しのシーケンスを視覚的に示します。 次のセクションでは、各関数の目的を詳しく説明します。

次の図は、通常の Visual Basic Windows フォーム アプリケーションのアプリケーション モデル呼び出しシーケンスを示しています。 `Sub Main` プロシージャで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> メソッドを呼び出すと、シーケンスが開始されます。

![アプリケーション モデル呼び出しシーケンスを示す図。](./media/extending-the-visual-basic-application-model/application-model-call-sequence.gif)

Visual Basic アプリケーション モデルでは、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> イベントと <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> イベントも提供されます。 次の図は、これらのイベントを発生させるメカニズムを示しています。

![StartupNextInstance イベントを発生させる OnStartupNextInstance メソッドを示す図。](./media/extending-the-visual-basic-application-model/raise-startupnextinstance-event.gif)

![UnhandledException イベントを発生させる OnUnhandledException メソッドを示す図。](./media/extending-the-visual-basic-application-model/raise-unhandledexception-event.gif)

## <a name="overriding-the-base-methods"></a>基本メソッドのオーバーライド

<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> メソッドでは、`Application` メソッドが実行される順序を定義します。 既定では、Windows フォーム アプリケーションの `Sub Main` プロシージャで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> メソッドが呼び出されます。

アプリケーションが通常のアプリケーション (複数インスタンス アプリケーション)、または単一インスタンス アプリケーションの最初のインスタンスである場合、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> メソッドでは、次の順序で `Overridable` メソッドが実行されます。

1. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>。 既定では、このメソッドで、メイン アプリケーション スレッドの視覚スタイル、テキスト表示スタイル、および現在のプリンシパルが設定され (アプリケーションが Windows 認証を使用している場合)、コマンドライン引数として `/nosplash` も `-nosplash` も使用されていない場合に、`ShowSplashScreen` が呼び出されます。

     この関数から `False` が返されると、アプリケーションの起動シーケンスが取り消されます。 これは、アプリケーションを実行するべきではない状況がある場合に便利です。

     <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> メソッドでは、次のメソッドが呼び出されます。

    1. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A>。 アプリケーションにスプラッシュ スクリーンが定義されているかどうかを判断し、定義されている場合は別のスレッドでスプラッシュ スクリーンを表示します。

         <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A> メソッドには、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A> プロパティに指定されたミリ秒間以上、スプラッシュ スクリーンを表示するコードが含まれます。 この機能を使用するには、**プロジェクト デザイナー**を使用して、アプリケーションにスプラッシュ スクリーンを追加する (これにより `My.Application.MinimumSplashScreenDisplayTime` プロパティが 2 秒に設定される) か、または <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> メソッドまたは <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> メソッドをオーバーライドするメソッドで、`My.Application.MinimumSplashScreenDisplayTime` プロパティを設定する必要があります。 詳細については、「<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>」を参照してください。

    2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>。 デザイナーに、スプラッシュ スクリーンを初期化するコードを生成させます。

         既定では、このメソッドは何も実行しません。 Visual Basic **プロジェクト デザイナー**で、アプリケーションのスプラッシュ スクリーンを選択すると、デザイナーでは、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A> プロパティをスプラッシュ スクリーン フォームの新しいインスタンスに設定するメソッドによって、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> メソッドがオーバーライドされます。

2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartup%2A>。 `Startup` イベントを発生させるための機能拡張ポイントを提供します。 この関数から `False` が返されると、アプリケーションの起動シーケンスが停止します。

     既定では、このメソッドで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> イベントが発生します。 イベント ハンドラーによって、イベント引数の <xref:System.ComponentModel.CancelEventArgs.Cancel> プロパティが `True` に設定された場合、メソッドで `False` が返され、アプリケーションの起動が取り消されます。

3. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnRun%2A>。 初期化が完了した後に、メイン アプリケーションの実行を開始する準備ができたときの開始点を提供します。

     既定では、Windows フォーム メッセージ ループに入る前に、このメソッドによって `OnCreateMainForm` メソッド (アプリケーションのメイン フォームを作成する) と `HideSplashScreen` (スプラッシュ スクリーンを閉じる) メソッドが呼び出されます。

    1. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>。 デザイナーがメイン フォームを初期化するコードを生成するための方法を提供します。

         既定では、このメソッドは何も実行しません。 ただし、Visual Basic **プロジェクト デザイナー**で、アプリケーションのメイン フォームを選択すると、デザイナーでは、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> プロパティをメイン フォームの新しいインスタンスに設定するメソッドによって、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> メソッドがオーバーライドされます。

    2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.HideSplashScreen%2A>。 アプリケーションにスプラッシュ スクリーンが定義されていて、それが開いている場合、このメソッドによってスプラッシュ スクリーンが閉じられます。

         既定では、このメソッドによってスプラッシュ スクリーンが閉じられます。

4. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A>。 アプリケーションの別のインスタンスが起動したときの、単一インスタンス アプリケーションの動作をカスタマイズする方法を提供します。

     既定では、このメソッドで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> イベントが発生します。

5. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnShutdown%2A>。 `Shutdown` イベントを発生させるための機能拡張ポイントを提供します。 メイン アプリケーションでハンドルされない例外が発生した場合、このメソッドは実行されません。

     既定では、このメソッドで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> イベントが発生します。

6. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnUnhandledException%2A>。 上記のいずれかのメソッドでハンドルされない例外が発生した場合に実行されます。

     既定では、デバッガーがアタッチされておらず、アプリケーションが `UnhandledException` イベントを処理している限り、このメソッドで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> イベントが発生します。

 アプリケーションが単一インスタンス アプリケーションであり、アプリケーションが既に実行中の場合、アプリケーションの後続のインスタンスでは、アプリケーションの元のインスタンスに対して <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A> メソッドが呼び出されてから、終了します。

 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance(Microsoft.VisualBasic.ApplicationServices.StartupNextInstanceEventArgs)> コンストラクターでは、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> プロパティが呼び出され、アプリケーションのフォームに使用するテキスト レンダリング エンジンが決定されます。 既定では、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> プロパティによって `False` が返されます。これは、GDI テキスト レンダリングエンジンが使用されることを示します。これは Visual Basic 2005 以降のバージョンの既定です。 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> プロパティが `True` を返すようにオーバーライドできます。これは、Visual Basic .NET 2002 および Visual Basic .NET 2003 の既定である GDI + テキスト レンダリング エンジンを使用することを示します。

## <a name="configuring-the-application"></a>アプリケーションの構成

 Visual Basic アプリケーション モデルの一部として、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> クラスには、アプリケーションを構成する保護されたプロパティが用意されています。 これらのプロパティは、実装するクラスのコンストラクターに設定する必要があります。

 既定の Windows フォーム プロジェクトでは、**プロジェクト デザイナー**によって、デザイナーの設定でプロパティを設定するコードが作成されます。 プロパティは、アプリケーションの起動時にのみ使用されます。アプリケーションの起動後に設定しても無効です。

|プロパティ|決定内容|プロジェクト デザイナーのアプリケーション ウィンドウの設定|
|---|---|---|
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.IsSingleInstance%2A>|アプリケーションを単一インスタンス アプリケーションと複数インスタンス アプリケーションのどちらとして実行するか。|**[単一インスタンスのアプリケーションを作成する]** チェックボックス|
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.EnableVisualStyles%2A>|アプリケーションで Windows XP に一致する視覚スタイルを使用するかどうか。|**[XP Visual スタイルを有効にする]** チェックボックス|
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SaveMySettingsOnExit%2A>|アプリケーションの終了時に、アプリケーションで、アプリケーションのユーザー設定の変更を自動的に保存するかどうか。|**[シャットダウン時に My.Settings を保存する]** チェックボックス|
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShutdownStyle%2A>|スタートアップ フォームが閉じたときや、最後のフォームが閉じたときなど、アプリケーションが終了する原因。|**[シャットダウン モード]** リスト|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>
- [Visual Basic アプリケーション モデルの概要](../development-with-my/overview-of-the-visual-basic-application-model.md)
- [[アプリケーション] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
