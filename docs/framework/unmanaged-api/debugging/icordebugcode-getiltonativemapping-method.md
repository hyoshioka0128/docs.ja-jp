---
title: ICorDebugCode::GetILToNativeMapping メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetILToNativeMapping
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetILToNativeMapping method [.NET Framework debugging]
ms.assetid: a8ecd8c8-9627-4356-9c6f-bd05e24637c0
topic_type:
- apiref
ms.openlocfilehash: 3de85626be6ae8e4769ac261f4de1479461417ec
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893540"
---
# <a name="icordebugcodegetiltonativemapping-method"></a>ICorDebugCode::GetILToNativeMapping メソッド
Microsoft 中間言語 (MSIL) オフセットからネイティブオフセットへのマッピングを表す "COR_DEBUG_IL_TO_NATIVE_MAP" インスタンスの配列を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetILToNativeMapping (  
    [in]  ULONG32    cMap,  
    [out] ULONG32    *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cMap`  
 [in] `map` 配列のサイズ。  
  
 `pcMap`  
 入出力`map`配列で返された実際の要素数へのポインター。  
  
 `map`  
 入出力構造体の`COR_DEBUG_IL_TO_NATIVE_MAP`配列。それぞれが MSIL オフセットからネイティブオフセットへのマッピングを表します。  
  
 返される要素の配列への順序はありません。  
  
## <a name="remarks"></a>解説  
 メソッド`GetILToNativeMapping`は、この "" コード "インスタンスが MSIL コードからコンパイルされた JUST-IN-TIME (JIT) コードを表している場合にのみ、意味のある結果を返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugCode インターフェイス](icordebugcode-interface1.md)
