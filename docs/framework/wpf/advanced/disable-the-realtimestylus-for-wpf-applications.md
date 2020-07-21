---
title: RealTimeStylus を無効にする
ms.date: 03/30/2017
ms.assetid: e0525309-5ede-4782-837d-dbf6e5554859
ms.openlocfilehash: c2500b494f76c85e4b23823a44a180d85d5092ff
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186077"
---
# <a name="disable-the-realtimestylus-for-wpf-applications"></a>WPF アプリケーションのリアルタイムなスタイラス入力を無効にする

Windows Presentation Foundation (WPF) には、Windows 7 のタッチ入力を処理するためのサポートが組み込まれています。 このサポートは、タブレット プラットフォームでの <xref:System.Windows.UIElement.OnStylusDown%2A>、<xref:System.Windows.UIElement.OnStylusUp%2A>、および <xref:System.Windows.UIElement.OnStylusMove%2A> イベントとしてのリアルタイム スタイラス入力によって行われます。 Windows 7 では、Win32 WM_TOUCH ウィンドウ メッセージとしてマルチタッチ入力も提供されます。 これらの 2 つの API を同じ HWND で同時に使用することはできません。 タブレット プラットフォームによるタッチ入力 (WPF アプリケーションの既定値) を有効にすると、WM_TOUCH メッセージは無効になります。 そのため、WM_TOUCH を使用して WPF ウィンドウからタッチ メッセージを受け取るには、WPF の組み込みスタイラス サポートを無効にする必要があります。 これは、WM_TOUCH を使用するコンポーネントをホストする WPF ウィンドウなどのシナリオに適用されます。  
  
 WPF によるスタイラス入力のリッスンを無効にするには、WPF ウィンドウによって追加されるすべてのタブレット サポートを削除します。  
  
## <a name="example"></a>例  
 次のサンプル コードでは、リフレクションを使用して既定のタブレット プラットフォームのサポートを削除する方法を示します。  
  
```csharp  
public static void DisableWPFTabletSupport()  
{  
    // Get a collection of the tablet devices for this window.
    TabletDeviceCollection devices = System.Windows.Input.Tablet.TabletDevices;  
  
    if (devices.Count > 0)  
    {
        // Get the Type of InputManager.  
        Type inputManagerType = typeof(System.Windows.Input.InputManager);  
  
        // Call the StylusLogic method on the InputManager.Current instance.  
        object stylusLogic = inputManagerType.InvokeMember("StylusLogic",  
                    BindingFlags.GetProperty | BindingFlags.Instance | BindingFlags.NonPublic,  
                    null, InputManager.Current, null);  
  
        if (stylusLogic != null)  
        {  
            //  Get the type of the stylusLogic returned from the call to StylusLogic.  
            Type stylusLogicType = stylusLogic.GetType();  
  
            // Loop until there are no more devices to remove.  
            while (devices.Count > 0)  
            {  
                // Remove the first tablet device in the devices collection.  
                stylusLogicType.InvokeMember("OnTabletRemoved",  
                        BindingFlags.InvokeMethod | BindingFlags.Instance | BindingFlags.NonPublic,  
                        null, stylusLogic, new object[] { (uint)0 });  
            }
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [スタイラスからの入力のインターセプト](intercepting-input-from-the-stylus.md)
