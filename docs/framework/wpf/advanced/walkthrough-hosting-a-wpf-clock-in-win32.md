---
title: 'チュートリアル: Win32 で WPF の時計をホストする'
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- interoperability [WPF], tutorials
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 555e55a7-0851-4ec8-b1c6-0acba7e9b648
ms.openlocfilehash: 0aecde96d182e12ab72b1a6cba129ab1d8a28391
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77123780"
---
# <a name="walkthrough-host-a-wpf-clock-in-win32"></a>チュートリアル: Win32 で WPF の時計をホストする

Win32 アプリケーション内に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を配置するには、<xref:System.Windows.Interop.HwndSource> を使用します。これで、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツを含む HWND を用意できます。 まず <xref:System.Windows.Interop.HwndSource> を作成し、CreateWindow のようなパラメーターを指定します。 次に、その中で必要な [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツについて <xref:System.Windows.Interop.HwndSource> に伝えます。 最後に、<xref:System.Windows.Interop.HwndSource> から HWND を取得します。 このチュートリアルでは、Win32 アプリケーション内に、オペレーティング システムの **[日付と時刻のプロパティ]** ダイアログを実装し直した混合 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

「[WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)」を参照してください

## <a name="how-to-use-this-tutorial"></a>このチュートリアルの使用方法

このチュートリアルでは、相互運用アプリケーションを作成するための重要な手順に焦点を当てています。 このチュートリアルはサンプル [Win32 の時計の相互運用性サンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/Win32Clock)を利用していますが、このサンプルは完成品のお手本です。 このチュートリアルでは、(実際はお持ちでないかもしれませんが) お持ちの既存の Win32 プロジェクトから始めて、ホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] をアプリケーションに追加する場合を仮定して手順を説明します。 完成品は [Win32 の時計の相互運用性サンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/Win32Clock)と比較することができます。

## <a name="a-walkthrough-of-windows-presentation-framework-inside-win32-hwndsource"></a>Win32 (HwndSource) 内の Windows Presentation Framework のチュートリアル

次の図は、このチュートリアルの完成品を示しています。

![[日付と時刻のプロパティ] ダイアログ ボックスが表示されたスクリーンショット。](./media/walkthrough-hosting-a-wpf-clock-in-win32/date-time-properties-dialog.png)

このダイアログを再現するには、Visual Studio で C++ Win32 プロジェクトを作成し、ダイアログ エディターを使用して次のものを作成します。

![再現した [日付と時刻のプロパティ] ダイアログ ボックス](./media/walkthrough-hosting-a-wpf-clock-in-win32/recreated-date-time-properties-dialog.png)

(<xref:System.Windows.Interop.HwndSource> を使用するために Visual Studio を使用する必要はありません。また、Win32 プログラムを作成するために C++ を使用する必要もありませんが、これはかなり一般的な方法であり、段階的なチュートリアルの説明に適しています)。

ダイアログに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計を配置するには、5 つの特定のサブ手順を実行する必要があります。

1. Visual Studio でプロジェクト設定を変更して、Win32 プロジェクトからマネージド コード ( **/clr**) を呼び出せるようにします。

2. 別の DLL に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page> を作成します。

3. その [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page> を <xref:System.Windows.Interop.HwndSource> 内に配置します。

4. <xref:System.Windows.Interop.HwndSource.Handle%2A> プロパティを使用して、その <xref:System.Windows.Controls.Page> の HWND を取得します。

5. Win32 を使用して、HWND をより大きな Win32 アプリケーション内のどこに配置するかを決定します

## <a name="clr"></a>/clr

最初の手順は、このアンマネージ Win32 プロジェクトを、マネージド コードを呼び出すことができるプロジェクトに変えることです。 /clr コンパイラ オプションを使用します。これで、使用する必要な DLL にリンクされされます。また、Main メソッドを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で使用できるように調整します。

C++ プロジェクト内でマネージド コードの使用を有効にするには:win32clock プロジェクトを右クリックし、 **[プロパティ]** を選択します。 **[全般]** プロパティ ページ (既定値) で、共通言語ランタイムのサポートを `/clr` に変更します。

次に、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に必要な次の DLL への参照を追加します。PresentationCore.dll、PresentationFramework.dll、System.dll、WindowsBase.dll、UIAutomationProvider.dll、UIAutomationTypes.dll (以下の手順では、オペレーティング システムが C: ドライブにインストールされていることを前提としています)。

1. win32clock プロジェクトを右クリックし、 **[参照]** を選択し、ダイアログ内で次の手順を実行します。

2. win32clock プロジェクトを右クリックし、 **[参照]** を選択します。

3. **[新しい参照の追加]** をクリックし、[参照] タブをクリックし、「C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationCore.dll」と入力して [OK] をクリックします。

4. 次の PresentationFramework.dll に対してこの手順を繰り返します。C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationFramework.dll。

5. 次の WindowsBase.dll に対してこの手順を繰り返します。C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\WindowsBase.dll。

6. 次の UIAutomationTypes.dll に対してこの手順を繰り返します。C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\UIAutomationTypes.dll。

7. 次の UIAutomationProvider.dll に対してこの手順を繰り返します。C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\UIAutomationProvider.dll。

8. **[新しい参照の追加]** をクリックし、System.dll を選択して **[OK]** をクリックします。

9. **[OK]** をクリックして、参照を追加するために win32clock の [プロパティ] ページを終了します。

 最後に、`STAThreadAttribute` を `_tWinMain` メソッドに追加して、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で使用できるようにします。

```cpp
[System::STAThreadAttribute]
int APIENTRY _tWinMain(HINSTANCE hInstance,
                     HINSTANCE hPrevInstance,
                     LPTSTR    lpCmdLine,
                     int       nCmdShow)
```

この属性を使用すると、コンポーネント オブジェクト モデル (COM) を初期化するときに、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] (および Windows フォーム) に必要なシングル スレッド アパートメント モデル (STA) を使用するように共通言語ランタイム (CLR) に指示することができます。

## <a name="create-a-windows-presentation-framework-page"></a>Windows Presentation Framework ページを作成する

次に、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page> を定義する DLL を作成します。 多くの場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page> をスタンドアロン アプリケーションとして作成し、それに従って [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 部分を記述してデバッグする方法が最も簡単です。 完了したら、プロジェクトを右クリックし、 **[プロパティ]** をクリックして、アプリケーションに移動し、出力の種類を Windows クラス ライブラリに変更することで、そのプロジェクトを DLL に変換することができます。

これで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dll プロジェクトを Win32 プロジェクト (2 つのプロジェクトを含む 1 つのソリューション) と組み合わせることができます。ソリューションを右クリックし、 **[既存プロジェクトの追加]** を選択します。

Win32 プロジェクトから [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dll を使用するには、参照を追加する必要があります。

1. win32clock プロジェクトを右クリックし、 **[参照]** を選択します。

2. **[新しい参照の追加]** をクリックします。

3. **[プロジェクト]** タブをクリックします。WPFClock を選択し、[OK] をクリックします。

4. **[OK]** をクリックして、参照を追加するために win32clock の [プロパティ] ページを終了します。

## <a name="hwndsource"></a>HwndSource

次に、<xref:System.Windows.Interop.HwndSource> を使用して、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page> を HWND のようにします。 次のコード ブロックを C++ ファイルに追加します。

```cpp
namespace ManagedCode
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Media;

    HWND GetHwnd(HWND parent, int x, int y, int width, int height) {
        HwndSource^ source = gcnew HwndSource(
            0, // class style
            WS_VISIBLE | WS_CHILD, // style
            0, // exstyle
            x, y, width, height,
            "hi", // NAME
            IntPtr(parent)        // parent window
            );

        UIElement^ page = gcnew WPFClock::Clock();
        source->RootVisual = page;
        return (HWND) source->Handle.ToPointer();
    }
}
}
```

 これは長いコードなので、いくつか説明を加えます。 すべての呼び出しを完全に修飾する必要がないように、最初の部分にはさまざまな句があります。

```cpp
namespace ManagedCode
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Media;
```

 次に、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のコンテンツを作成し、それを <xref:System.Windows.Interop.HwndSource> で囲み、HWND を返す関数を定義します。

```cpp
HWND GetHwnd(HWND parent, int x, int y, int width, int height) {
```

まず、CreateWindow と同様のパラメーターを持つ <xref:System.Windows.Interop.HwndSource> を作成します。

```cpp
HwndSource^ source = gcnew HwndSource(
    0, // class style
    WS_VISIBLE | WS_CHILD, // style
    0, // exstyle
    x, y, width, height,
    "hi", // NAME
    IntPtr(parent) // parent window
);
```

次に、コンストラクターを呼び出して [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツ クラスを作成します。

```cpp
UIElement^ page = gcnew WPFClock::Clock();
```

次に、ページを <xref:System.Windows.Interop.HwndSource> に接続します。

```cpp
source->RootVisual = page;
```

 最後の行で、<xref:System.Windows.Interop.HwndSource> の HWND を返します。

```cpp
return (HWND) source->Handle.ToPointer();
```

## <a name="positioning-the-hwnd"></a>Hwnd の配置

これで、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計を含む HWND が完成したので、その HWND を Win32 ダイアログ内に配置する必要があります。 HWND を配置する場所がわかっている場合は、先ほど定義した `GetHwnd` 関数にそのサイズと場所を渡します。 ただし、リソース ファイルを使用してダイアログを定義しているため、HWND のどこに配置されているかは正確にはわかりません。 Visual Studio のダイアログ エディターを使用して、Win32 STATIC コントロールを時計の移動先 ("Insert clock here" (ここに時計を挿入)) に配置し、それを使用して [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計を配置できます。

WM_INITDIALOG を処理する場合、`GetDlgItem` を使用してプレースホルダー STATIC の HWND を取得します。

```cpp
HWND placeholder = GetDlgItem(hDlg, IDC_CLOCK);
```

次に、そのプレースホルダー STATIC のサイズと位置を計算し、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計をその場所に配置できるようにします。

RECT 四角形;

```cpp
GetWindowRect(placeholder, &rectangle);
int width = rectangle.right - rectangle.left;
int height = rectangle.bottom - rectangle.top;
POINT point;
point.x = rectangle.left;
point.y = rectangle.top;
result = MapWindowPoints(NULL, hDlg, &point, 1);
```

次に、プレースホルダー STATIC を非表示にします。

```cpp
ShowWindow(placeholder, SW_HIDE);
```

そして、その場所に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計の HWND を作成します。

```cpp
HWND clock = ManagedCode::GetHwnd(hDlg, point.x, point.y, width, height);
```

このチュートリアルをおもしろくするために、また実際の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計を再現するために、この時点で [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計コントロールを作成する必要があります。 主にマークアップで、コードビハインドにいくつかのイベント ハンドラーを使用するだけで、これを行うことができます。 このチュートリアルは相互運用に関するものであり、コントロールの設計に関するものではないため、ここでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の時計の完成したコードをコード ブロックとして提供しています。ビルドに関する個別の指示や各部分の意味については説明しません。 このコードを自由に試して、コントロールの外観や機能を変更してみてください。

マークアップは次のとおりです。

[!code-xaml[Win32Clock#AllClockXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml#allclockxaml)]

そして、関連するコードビハインドは次のとおりです。

[!code-csharp[Win32Clock#AllClockCS](~/samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml.cs#allclockcs)]

最終的な結果は次のようになります。

![最終的な結果の [日付と時刻のプロパティ] ダイアログ ボックス](./media/walkthrough-hosting-a-wpf-clock-in-win32/final-result-date-time-properties-dialog.png)

最終的な結果をこのスクリーンショットの生成に使ったコードと比較するには、[Win32 の時計の相互運用性サンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/Win32Clock)を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.HwndSource>
- [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)
- [Win32 クロック相互運用のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/Win32Clock)
