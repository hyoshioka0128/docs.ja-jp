---
title: FilterInputMessage
ms.date: 03/30/2017
helpviewer_keywords:
- raw input [WPF]
- FilterInputMessage method [WPF]
ms.assetid: 4d74c6cf-7d1d-49ff-96c1-231340ce54f5
ms.openlocfilehash: 1453946766e33843ae9e56f7a7f4dbf1678b81b5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991382"
---
# <a name="filterinputmessage"></a>FilterInputMessage
E_NOTIMPL が返されない限り、メッセージを受信するたびに PresentationHost.exe によって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FilterInputMessage( [in] MSG* pMsg ) ;  
```  
  
## <a name="parameters"></a>パラメーター  
 `pMsg`  
  
 [in] 未加工入力を取得するウィンドウに送信される WM_INPUT メッセージ。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 HRESULT:  
  
 S_OK - フィルターはメッセージを処理せず、それ以降の処理は実行されることがあります。  
  
 S_FALSE - フィルターはこのメッセージを処理しました。それ以降の処理は実行されません。  
  
 E_NOTIMPL – この値が返される場合、[FilterInputMessage](filterinputmessage.md) は再度呼び出されません。 この値は、カスタムの進行状況の提供のみを対象とするホスト アプリケーションから返されることがあります。PresentationHost.exe へのエラー ユーザー インターフェイスは、PresentationHost.exe からの未加工の入力メッセージの転送を対象としていません。  
  
## <a name="remarks"></a>Remarks  
 PresentationHost.exe は、キーボード、マウス、およびリモート コントロールなどのさまざまな未加工入力デバイスのターゲットになります。 場合によって、ホスト アプリケーションでの動作は PresentationHost.exe で使用される入力に依存します。 たとえば、ホスト アプリケーションは、特定のユーザー インターフェイス要素を表示するかどうかを判断するために、特定の入力メッセージの受信に依存することがあります。  
  
 これらの動作を提供するためにホスト アプリケーションが必要な入力メッセージを受信できるようにするため、PresentationHost.exe では、[FilterInputMessage](filterinputmessage.md) を呼び出すことで、ホストされているアプリケーションに適切な未加工の入力メッセージが転送されます。  
  
 ホストされるアプリケーションでは、[GetRawInputDevices](getrawinputdevices.md) によって返される未加工の入力デバイス (ヒューマン インターフェイス デバイス) のセットを登録することで、未加工の入力メッセージを受信します。  
  
## <a name="see-also"></a>関連項目

- [WM_INPUT メッセージ](/windows/desktop/inputdev/wm-input)
