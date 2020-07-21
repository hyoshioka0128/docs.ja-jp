---
title: Win32 コンテンツのホスト
ms.date: 03/30/2017
helpviewer_keywords:
- interoperability [WPF], tutorials
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 3cc8644a-34f3-4082-9ddc-77623e4df2d8
ms.openlocfilehash: c0c62f1999feaf591c512314515f01e83fa12591
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052092"
---
# <a name="hosting-win32-content-in-wpf"></a>WPF での Win32 コンテンツのホスト

## <a name="prerequisites"></a>必須コンポーネント

「[WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)」を参照してください

## <a name="a-walkthrough-of-win32-inside-windows-presentation-framework-hwndhost"></a>Windows Presentation Framework (HwndHost) 内の Win32 のチュートリアル

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション内で Win32 コンテンツを再利用するには、<xref:System.Windows.Interop.HwndHost> を使用します。これは、HWND を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツのようにするコントロールです。 <xref:System.Windows.Interop.HwndSource> と同様に、<xref:System.Windows.Interop.HwndHost> は簡単に使用できます。<xref:System.Windows.Interop.HwndHost> から派生し、`BuildWindowCore` および `DestroyWindowCore` メソッドを実装し、<xref:System.Windows.Interop.HwndHost> 派生クラスをインスタンス化して [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション内に配置します。

Win32 ロジックが既にコントロールとしてパッケージ化されている場合、`BuildWindowCore` の実装は単なる `CreateWindow` の呼び出しです。 たとえば、C++ で Win32 LISTBOX コントロールを作成するには、次のようにします。

```cpp
virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {
    HWND handle = CreateWindowEx(0, L"LISTBOX",
    L"this is a Win32 listbox",
    WS_CHILD | WS_VISIBLE | LBS_NOTIFY
    | WS_VSCROLL | WS_BORDER,
    0, 0, // x, y
    30, 70, // height, width
    (HWND) hwndParent.Handle.ToPointer(), // parent hwnd
    0, // hmenu
    0, // hinstance
    0); // lparam

    return HandleRef(this, IntPtr(handle));
}

virtual void DestroyWindowCore(HandleRef hwnd) override {
    // HwndHost will dispose the hwnd for us
}
```

ただし、Win32 コードがそれほど自己完結型ではない場合はどうでしょうか。 その場合は、Win32 ダイアログ ボックスを作成し、そのコンテンツをより大きな [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションに埋め込むことができます。 このサンプルでは、これを Visual Studio および C++ で示していますが、別の言語またはコマンド ラインで行うこともできます。

まず C++ DLL プロジェクトにコンパイルされるシンプルなダイアログから始めます。

次に、より大きな [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションにダイアログを導入します。

- DLL をマネージドとしてコンパイルする (`/clr`)

- ダイアログをコントロールに変換する

- `BuildWindowCore` メソッドと `DestroyWindowCore` メソッドを使用して <xref:System.Windows.Interop.HwndHost> の派生クラスを定義する

- ダイアログ キーを処理するために `TranslateAccelerator` メソッドをオーバーライドする

- タブ移動をサポートするために `TabInto` メソッドをオーバーライドする

- ニーモニックをサポートするために `OnMnemonic` メソッドをオーバーライドする

- <xref:System.Windows.Interop.HwndHost> サブクラスをインスタンス化し、適切な [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素の下に配置します

### <a name="turn-the-dialog-into-a-control"></a>ダイアログをコントロールに変換する

WS_CHILD および DS_CONTROL スタイルを使用して、ダイアログ ボックスを子 HWND に変えることができます。 ダイアログが定義されているリソース ファイル (.rc) に移動し、ダイアログの定義の先頭を見つけます。

```text
IDD_DIALOG1 DIALOGEX 0, 0, 303, 121
STYLE DS_SETFONT | DS_MODALFRAME | DS_FIXEDSYS | WS_POPUP | WS_CAPTION | WS_SYSMENU
```

2 行目を次のように変更します。

```text
STYLE DS_SETFONT | WS_CHILD | WS_BORDER | DS_CONTROL
```

このアクションでは、自己完結型のコントロールに完全にパッケージ化されません。Win32 で特定のメッセージを処理できるように、`IsDialogMessage()` を呼び出す必要がありますが、このコントロールの変更により、これらのコントロールを別の HWND 内に簡単に配置できるようになります。

## <a name="subclass-hwndhost"></a>サブクラス HwndHost

次の名前空間をインポートします。

```cpp
namespace ManagedCpp
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Input;
    using namespace System::Windows::Media;
    using namespace System::Runtime::InteropServices;
```

次に、<xref:System.Windows.Interop.HwndHost> の派生クラスを作成し、`BuildWindowCore` および `DestroyWindowCore` メソッドをオーバーライドします。

```cpp
public ref class MyHwndHost : public HwndHost, IKeyboardInputSink {
    private:
        HWND dialog;

    protected:
        virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {
            InitializeGlobals();
            dialog = CreateDialog(hInstance,
                MAKEINTRESOURCE(IDD_DIALOG1),
                (HWND) hwndParent.Handle.ToPointer(),
                (DLGPROC) About);
            return HandleRef(this, IntPtr(dialog));
        }

        virtual void DestroyWindowCore(HandleRef hwnd) override {
            // hwnd will be disposed for us
        }
```

ここでは、`CreateDialog` を使用して、実際にコントロールであるダイアログ ボックスを作成します。 これは DLL 内で呼び出される最初のメソッドの 1 つであるため、後で定義する `InitializeGlobals()` という関数を呼び出して、標準の Win32 初期化を行う必要があります。

```cpp
bool initialized = false;
    void InitializeGlobals() {
        if (initialized) return;
        initialized = true;

        // TODO: Place code here.
        MSG msg;
        HACCEL hAccelTable;

        // Initialize global strings
        LoadString(hInstance, IDS_APP_TITLE, szTitle, MAX_LOADSTRING);
        LoadString(hInstance, IDC_TYPICALWIN32DIALOG, szWindowClass, MAX_LOADSTRING);
        MyRegisterClass(hInstance);
```

### <a name="override-translateaccelerator-method-to-handle-dialog-keys"></a>ダイアログキーを処理するために TranslateAccelerator メソッドをオーバーライドする

ここでこのサンプルを実行すると、ダイアログ コントロールが表示されますが、ダイアログ ボックスを機能するダイアログ ボックスにするキーボード処理はすべて無視されます。 ここで、`TranslateAccelerator` 実装 (<xref:System.Windows.Interop.HwndHost> に実装されているインターフェイスである `IKeyboardInputSink` から継承されます) をオーバーライドする必要があります。 このメソッドは、アプリケーションが WM_KEYDOWN および WM_SYSKEYDOWN を受け取ったときに呼び出されます。

```cpp
#undef TranslateAccelerator
        virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,
            ModifierKeys modifiers) override
        {
            ::MSG m = ConvertMessage(msg);

            // Win32's IsDialogMessage() will handle most of our tabbing, but doesn't know
            // what to do when it reaches the last tab stop
            if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {
                HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
                HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
                TraversalRequest^ request = nullptr;

                if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {
                    // this code should work, but there’s a bug with interop shift-tab in current builds
                    request = gcnew TraversalRequest(FocusNavigationDirection::Last);
                }
                else if (!GetKeyState(VK_SHIFT) && GetFocus() == lastTabStop) {
                    request = gcnew TraversalRequest(FocusNavigationDirection::Next);
                }

                if (request != nullptr)
                    return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);

            }

            // Only call IsDialogMessage for keys it will do something with.
            if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {
                switch (m.wParam) {
                    case VK_TAB:
                    case VK_LEFT:
                    case VK_UP:
                    case VK_RIGHT:
                    case VK_DOWN:
                    case VK_EXECUTE:
                    case VK_RETURN:
                    case VK_ESCAPE:
                    case VK_CANCEL:
                        IsDialogMessage(dialog, &m);
                        // IsDialogMessage should be called ProcessDialogMessage --
                        // it processes messages without ever really telling you
                        // if it handled a specific message or not
                        return true;
                }
            }

            return false; // not a key we handled
        }
```

これには多くのコードが 1 つにまとめられているため、より詳細な説明を使用できます。 1 つ目は、C++ および C++ マクロを使用するコードです。winuser.h で定義されている `TranslateAccelerator` という名前のマクロが既に存在することに注意する必要があります。

```cpp
#define TranslateAccelerator  TranslateAcceleratorW
```

そのため、`TranslateAcceleratorW` メソッドではなく、必ず `TranslateAccelerator` メソッドを定義してください。

同様に、アンマネージド winuser.h MSG とマネージド `Microsoft::Win32::MSG` 構造体の両方があります。 C++ の `::` 演算子を使用して、2 つを区別することができます。

```cpp
virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,
    ModifierKeys modifiers) override
{
    ::MSG m = ConvertMessage(msg);
}
```

いずれの MSG にも同じデータがありますが、アンマネージドの定義を使用した方が簡単なときがあります。そのため、このサンプルでは、見てすぐわかる変換ルーチンを定義できます。

```cpp
::MSG ConvertMessage(System::Windows::Interop::MSG% msg) {
    ::MSG m;
    m.hwnd = (HWND) msg.hwnd.ToPointer();
    m.lParam = (LPARAM) msg.lParam.ToPointer();
    m.message = msg.message;
    m.wParam = (WPARAM) msg.wParam.ToPointer();

    m.time = msg.time;

    POINT pt;
    pt.x = msg.pt_x;
    pt.y = msg.pt_y;
    m.pt = pt;

    return m;
}
```

`TranslateAccelerator` に戻ります。 基本的な原則は、できるだけ多くの作業を行うために Win32 関数 `IsDialogMessage` を呼び出すことですが、`IsDialogMessage` ではダイアログの外部にはアクセスできません。 ユーザーが Tab キーを使ってダイアログ内を移動するときに、タブ移動がダイアログの最後のコントロールを過ぎた場合に、`IKeyboardInputSite::OnNoMoreStops` を呼び出してフォーカスを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の部分に設定する必要があります。

```cpp
// Win32's IsDialogMessage() will handle most of the tabbing, but doesn't know
// what to do when it reaches the last tab stop
if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {
    HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
    HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
    TraversalRequest^ request = nullptr;

    if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {
        request = gcnew TraversalRequest(FocusNavigationDirection::Last);
    }
    else if (!GetKeyState(VK_SHIFT) && GetFocus() ==  lastTabStop) { {
        request = gcnew TraversalRequest(FocusNavigationDirection::Next);
    }

    if (request != nullptr)
        return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);
}
```

最後に、`IsDialogMessage` を呼び出します。 ただし、`TranslateAccelerator` メソッドの役割の 1 つは、キー入力を処理したかどうかを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に伝えることです。 これを処理しなかった場合、アプリケーションの残りの部分で、入力イベントのトンネリングとバブリングが発生する可能性があります。 ここでは、キーボードのメッセージ処理の癖と Win32 の入力アーキテクチャの性質を明らかにします。 残念ながら、どのような方法でも、`IsDialogMessage` から特定のキー入力を処理するかどうかは返されません。 さらに悪いことに、処理してはならないキー入力で `DispatchMessage()` が呼び出されます。  そのため、`IsDialogMessage` をリバースエンジニアリングして、処理することがわかっているキーに対してのみ呼び出す必要があります。

```cpp
// Only call IsDialogMessage for keys it will do something with.
if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {
    switch (m.wParam) {
        case VK_TAB:
        case VK_LEFT:
        case VK_UP:
        case VK_RIGHT:
        case VK_DOWN:
        case VK_EXECUTE:
        case VK_RETURN:
        case VK_ESCAPE:
        case VK_CANCEL:
            IsDialogMessage(dialog, &m);
            // IsDialogMessage should be called ProcessDialogMessage --
            // it processes messages without ever really telling you
            // if it handled a specific message or not
            return true;
    }
```

### <a name="override-tabinto-method-to-support-tabbing"></a>タブ移動をサポートするために TabInto メソッドをオーバーライドする

これで `TranslateAccelerator` を実装したので、ユーザーは Tab キーを使ってダイアログ ボックス内を移動し、そこからより大きな [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションにタブ移動できるようになります。 ただし、ユーザーがダイアログ ボックスに戻ることはできません。 これを解決するには、`TabInto` をオーバーライドします。

```cpp
public:
    virtual bool TabInto(TraversalRequest^ request) override {
        if (request->FocusNavigationDirection == FocusNavigationDirection::Last) {
            HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
            SetFocus(lastTabStop);
        }
        else {
            HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
            SetFocus(firstTabStop);
        }
        return true;
    }
```

`TraversalRequest` パラメーターを使用すると、タブ操作が Tab キーか Shift + Tab キーのどちらであるかがわかります。

### <a name="override-onmnemonic-method-to-support-mnemonics"></a>ニーモニックをサポートするするために OnMnemonic メソッドをオーバーライドする

キーボードの処理はほぼ完了していますが、不足していることが 1 つあります。ニーモニックが機能しないことです。 ユーザーが Alt + F キーを押した場合、フォーカスは [First name:]\(名\) 編集ボックスにジャンプしません。 そのため、`OnMnemonic` メソッドをオーバーライドします。

```cpp
virtual bool OnMnemonic(System::Windows::Interop::MSG% msg, ModifierKeys modifiers) override {
    ::MSG m = ConvertMessage(msg);

    // If it's one of our mnemonics, set focus to the appropriate hwnd
    if (msg.message == WM_SYSCHAR && GetKeyState(VK_MENU /*alt*/)) {
        int dialogitem = 9999;
        switch (m.wParam) {
            case 's': dialogitem = IDOK; break;
            case 'c': dialogitem = IDCANCEL; break;
            case 'f': dialogitem = IDC_EDIT1; break;
            case 'l': dialogitem = IDC_EDIT2; break;
            case 'p': dialogitem = IDC_EDIT3; break;
            case 'a': dialogitem = IDC_EDIT4; break;
            case 'i': dialogitem = IDC_EDIT5; break;
            case 't': dialogitem = IDC_EDIT6; break;
            case 'z': dialogitem = IDC_EDIT7; break;
        }
        if (dialogitem != 9999) {
            HWND hwnd = GetDlgItem(dialog, dialogitem);
            SetFocus(hwnd);
            return true;
        }
    }
    return false; // key unhandled
};
```

ここで `IsDialogMessage` を呼び出してみましょう。  前と同じ問題があります。コードでキー入力を処理されたかどうかを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コードに通知する必要がありますが、`IsDialogMessage` ではそれを行うことができません。 また、2 つ目の問題もあります。フォーカスされた HWND がダイアログ ボックス内にない場合、`IsDialogMessage` ではニーモニックの処理が拒否されるためです。

### <a name="instantiate-the-hwndhost-derived-class"></a>HwndHost 派生クラスをインスタンス化する

キーとタブが適切にサポートされたので、最後に、<xref:System.Windows.Interop.HwndHost> をより大きな[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションに配置できます。 メイン アプリケーションが [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で記述されている場合、適切な場所に配置する最も簡単な方法は、<xref:System.Windows.Interop.HwndHost> を配置する場所に空の <xref:System.Windows.Controls.Border> 要素を配置しておくことです。 ここでは、`insertHwndHostHere` という名前の <xref:System.Windows.Controls.Border> を作成します。

```xaml
<Window x:Class="WPFApplication1.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Windows Presentation Framework Application"
    Loaded="Window1_Loaded"
    >
    <StackPanel>
        <Button Content="WPF button"/>
        <Border Name="insertHwndHostHere" Height="200" Width="500"/>
        <Button Content="WPF button"/>
    </StackPanel>
</Window>
```

残りの作業は、コード シーケンス内の適切な場所を見つけて <xref:System.Windows.Interop.HwndHost> をインスタンス化し、それを <xref:System.Windows.Controls.Border> に接続することだけです。 この例では、<xref:System.Windows.Window> 派生クラスのコンストラクター内に配置します。

```csharp
public partial class Window1 : Window {
    public Window1() {
    }

    void Window1_Loaded(object sender, RoutedEventArgs e) {
        HwndHost host = new ManagedCpp.MyHwndHost();
        insertHwndHostHere.Child = host;
    }
}
```

次のようになります。

![実行中の WPF アプリのスクリーンショット。](./media/hosting-win32-content-in-wpf/windows-presentation-foundation-application.png)

## <a name="see-also"></a>関連項目

- [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)
