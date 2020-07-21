---
title: LoadFromHistory 関数 - WPF アンマネージ API リファレンス
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- LoadFromHistory
api_location:
- PresentationHost_v0400.dll
ms.assetid: d037c062-a911-4949-b251-ccd3e48b1d17
ms.openlocfilehash: be9b8658614e678b4370044a753554859d230fed
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141576"
---
# <a name="loadfromhistory-function-wpf-unmanaged-api-reference"></a>LoadFromHistory 関数 (WPF アンマネージ API リファレンス)
この API は、Windows Presentation Foundation (WPF) インフラストラクチャをサポートしますが、独自に作成したコードから直接使用するためのものではありません。  
  
 ウィンドウの管理のために Windows Presentation Foundation (WPF) インフラストラクチャによって使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LoadFromHistory_export(  
        IStream* pHistoryStream,
        IBindCtx* pBindCtx  
)  
```  
  
## <a name="parameters"></a>パラメーター  
 pHistoryStream  
 履歴情報のストリームへのポインター。  
  
 pBindCtx  
 バインド コンテキストへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** 「[.NET Framework システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **DLL:**  
  
 .NET Framework 3.0 および 3.5 の場合: PresentationHostDLL.dll  
  
 .NET Framework 4 以降の場合: PresentationHost_v0400.dll  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [WPF のアンマネージ API リファレンス](wpf-unmanaged-api-reference.md)
