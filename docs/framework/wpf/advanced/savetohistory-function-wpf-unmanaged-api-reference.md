---
title: SaveToHistory 関数 - WPF アンマネージ API リファレンス
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- SaveToHistory
api_location:
- PresentationHost_v0400.dll
ms.assetid: 6dd101a3-44ad-4143-b228-772156f9b8ff
ms.openlocfilehash: 7337e5dc23a3dce5de8270902bce228c49bc6edb
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76731750"
---
# <a name="savetohistory-function-wpf-unmanaged-api-reference"></a>SaveToHistory 関数 (WPF アンマネージ API リファレンス)
この API は、Windows Presentation Foundation (WPF) インフラストラクチャをサポートしますが、独自に作成したコードから直接使用するためのものではありません。  
  
 ウィンドウの管理のために Windows Presentation Foundation (WPF) インフラストラクチャによって使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SaveToHistory(  
   __in_ecount(1) IStream* pHistoryStream  
)  
```  
  
## <a name="parameters"></a>パラメーター  
 pHistoryStream  
 履歴ストリームへのポインター。  
  
## <a name="requirements"></a>必要条件  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** 「[.NET Framework システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **DLL:**  
  
 .NET Framework 3.0 および 3.5 の場合:PresentationHostDLL.dll  
  
 .NET Framework 4 以降の場合:PresentationHost_v0400.dll  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [WPF のアンマネージ API リファレンス](wpf-unmanaged-api-reference.md)
