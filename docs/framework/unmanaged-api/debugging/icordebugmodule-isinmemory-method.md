---
title: ICorDebugModule::IsInMemory メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule.IsInMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::IsInMemory
helpviewer_keywords:
- IsInMemory method [.NET Framework debugging]
- ICorDebugModule::IsInMemory method [.NET Framework debugging]
ms.assetid: 89940711-98e7-4aa6-bffc-5e39e91e1b7d
topic_type:
- apiref
ms.openlocfilehash: c5fa55a84ed8907a5072f6099c3bf02cd6d78683
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213128"
---
# <a name="icordebugmoduleisinmemory-method"></a>ICorDebugModule::IsInMemory メソッド
このモジュールがメモリ内にのみ存在するかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsInMemory(  
    [out] BOOL *pInMemory  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pInMemory`  
 [出力] `true`このモジュールがメモリ内にのみ存在する場合は、それ以外の場合は `false` 。  
  
## <a name="remarks"></a>Remarks  
 共通言語ランタイム (CLR) では、未加工のバイトストリームからのモジュールの読み込みがサポートされています。 このようなモジュールは*メモリ内モジュール*と呼ばれ、ディスク上には存在しません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
