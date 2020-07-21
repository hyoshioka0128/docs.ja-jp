---
title: SetFakeActiveWindow 関数 - WPF アンマネージ API リファレンス
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- SetFakeActiveWindow
api_location:
- PresentationHost_v0400.dll
ms.assetid: a69118be-63b0-445c-9fb6-ab8cc958e531
ms.openlocfilehash: 9282ec6f4c6fb9c1410ca07e707db98a02d0b02a
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76731727"
---
# <a name="setfakeactivewindow-function-wpf-unmanaged-api-reference"></a>SetFakeActiveWindow 関数 (WPF アンマネージ API リファレンス)
この API は、Windows Presentation Foundation (WPF) インフラストラクチャをサポートしますが、独自に作成したコードから直接使用するためのものではありません。  
  
 ウィンドウの管理のために Windows Presentation Foundation (WPF) インフラストラクチャによって使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall SetFakeActiveWindow(  
   HWND hwnd  
)  
```  
  
## <a name="parameters"></a>パラメーター  
 hwnd  
 ウィンドウ ハンドル。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** 「[.NET Framework システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **DLL:** PresentationHost_v0400.dll  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [WPF のアンマネージ API リファレンス](wpf-unmanaged-api-reference.md)
