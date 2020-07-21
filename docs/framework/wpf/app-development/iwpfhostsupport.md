---
title: IWpfHostSupport
ms.date: 03/30/2017
helpviewer_keywords:
- IWpfHostSupport interface [WPF]
ms.assetid: cc5a0281-de81-4cc1-87e4-0e46b1a811e9
ms.openlocfilehash: e3edd7f7080562d03453898dba7a9326561803b5
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77124196"
---
# <a name="iwpfhostsupport"></a>IWpfHostSupport
PresentationHost.exe を使用して [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] コンテンツをホストするアプリケーションでは、このインターフェイスを実装して、ホストと PresentationHost.exe の間の統合ポイントを提供します。  
  
## <a name="remarks"></a>Remarks  
 Web ブラウザーなどの Win32 アプリケーションでは、XAML ブラウザー アプリケーション (XBAP) や Loose XAML などの WPF コンテンツをホストできます。 WPF コンテンツをホストするには、Win32 アプリケーションで [WebBrowser コントロール](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752040(v=vs.85))のインスタンスを作成します。 ホストされるためには、WPF で PresentationHost.exe のインスタンスを作成します。このインスタンスで、[WebBrowser コントロール](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752040(v=vs.85))に表示するため、ホストされる WPF コンテンツをホストに提供します。  
  
 `IWpfHostSupport` によって有効になる統合により、PresentationHost.exe では次のことを行うことができます。  
  
- ホスト アプリケーションに必要な生入力デバイス (ヒューマン インターフェイス デバイス) を検出して登録します。  
  
- 登録されている生入力デバイスから入力メッセージを受け取り、適切なメッセージをホスト アプリケーションに転送します。  
  
- ホスト アプリケーションで、進行状況とエラーのカスタム ユーザー インターフェイスを照会します。  
  
> [!NOTE]
> この API は、ローカル クライアント コンピューターでの使用のみを目的とし、サポートされています。  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|[GetRawInputDevices](getrawinputdevices.md)|PresentationHost.exe が、ホスト アプリケーションに必要な未加工入力デバイス (ヒューマン インターフェイス デバイス) を検出できるようにします。|  
|[FilterInputMessage](filterinputmessage.md)|E_NOTIMPL が返されない限り、メッセージを受信するたびに PresentationHost.exe によって呼び出されます。|  
|[GetCustomUI](getcustomui.md)|既定では、PresentationHost.exe によって、WPF コンテンツが配置されるときに表示される、配置の進行状況と配置エラーの独自のユーザー インターフェイスが提供されます。|
