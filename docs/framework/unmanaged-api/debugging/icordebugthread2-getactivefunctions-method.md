---
title: ICorDebugThread2::GetActiveFunctions メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetActiveFunctions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetActiveFunctions
helpviewer_keywords:
- GetActiveFunctions method [.NET Framework debugging]
- ICorDebugThread2::GetActiveFunctions method [.NET Framework debugging]
ms.assetid: 27fae01a-ecec-423a-973e-24f8de55826c
topic_type:
- apiref
ms.openlocfilehash: e064a7db131a671adc4d0b6df522f3456e3a31d5
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83377152"
---
# <a name="icordebugthread2getactivefunctions-method"></a>ICorDebugThread2::GetActiveFunctions メソッド
このスレッドの各フレームのアクティブな関数に関する情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetActiveFunctions (  
    [in]   ULONG32             cFunctions,  
    [out]  ULONG32             *pcFunctions,  
    [in, out, size_is(cFunctions), length_is(*pcFunctions)]  
        COR_ACTIVE_FUNCTION    pFunctions[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cFunctions`  
 [in] `pFunctions` 配列のサイズ。  
  
 `pcFunctions`  
 入出力配列で返されたオブジェクトの数へのポインター `pFunctions` 。 返されるオブジェクトの数は、スタック上のマネージフレームの数と同じになります。  
  
 `pFunctions`  
 [入力、出力]COR_ACTIVE_FUNCTION オブジェクトの配列。各オブジェクトには、このスレッドのフレーム内のアクティブな関数に関する情報が含まれています。  
  
 最初の要素はリーフフレームに使用され、その後スタックのルートに戻ります。  
  
## <a name="remarks"></a>Remarks  
 `pFunctions`入力時にが null の場合、 `GetActiveFunctions` スタック上の関数の数だけを返します。 つまり、 `pFunctions` 入力時にが null の場合、は `GetActiveFunctions` でのみ値を返し `pcFunctions` ます。  
  
 この `GetActiveFunctions` メソッドは、スタックトレース内のフレームから同じ情報を取得することを目的とした最適化として使用されます。また、完全なスタックトレースでは、このメソッドに対しては、表示されないフレームオブジェクトを持つフレームだけを含みます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
