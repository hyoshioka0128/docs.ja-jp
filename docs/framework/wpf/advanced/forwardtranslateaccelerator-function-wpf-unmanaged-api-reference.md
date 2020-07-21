---
title: ForwardTranslateAccelerator 関数 - WPF アンマネージド API リファレンス
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ForwardTranslateAccelerator
api_location:
- PresentationHost_v0400.dll
ms.assetid: fff47a86-9d9f-4176-9530-10e1876e393f
ms.openlocfilehash: a0a01be3000dc53df7855cb74015ba1164206838
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186631"
---
# <a name="forwardtranslateaccelerator-function-wpf-unmanaged-api-reference"></a>ForwardTranslateAccelerator 関数 (WPF アンマネージド API リファレンス)
この API は、Windows Presentation Foundation (WPF) インフラストラクチャをサポートしますが、独自に作成したコードから直接使用するためのものではありません。  
  
 ウィンドウの管理のために Windows Presentation Foundation (WPF) インフラストラクチャによって使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ForwardTranslateAccelerator(  
   MSG* pMsg,
   VARIANT_BOOL appUnhandled  
)  
```  
  
## <a name="parameters"></a>パラメーター  
 pMsg  
 メッセージへのポインター。  
  
 appUnhandled  
 アプリは入力メッセージを処理する機会を既に与えられたがメッセージを処理していない場合は `true`。それ以外の場合は `false`。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** 「[.NET Framework システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **DLL:**  
  
 .NET Framework 3.0 および 3.5 の場合: PresentationHostDLL.dll  
  
 .NET Framework 4 以降の場合: PresentationHost_v0400.dll  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [WPF のアンマネージ API リファレンス](wpf-unmanaged-api-reference.md)
