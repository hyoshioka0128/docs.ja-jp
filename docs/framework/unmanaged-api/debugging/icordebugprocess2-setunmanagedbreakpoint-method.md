---
title: ICorDebugProcess2::SetUnmanagedBreakpoint メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetUnmanagedBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint
helpviewer_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint method [.NET Framework debugging]
- SetUnmanagedBreakpoint method [.NET Framework debugging]
ms.assetid: 93829d15-d942-4e2d-b7a4-dfc9d7fb96be
topic_type:
- apiref
ms.openlocfilehash: 6b9396d03892f29e3698af90856d0c0023dc628a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213466"
---
# <a name="icordebugprocess2setunmanagedbreakpoint-method"></a>ICorDebugProcess2::SetUnmanagedBreakpoint メソッド
指定したネイティブイメージオフセットにアンマネージブレークポイントを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetUnmanagedBreakpoint (  
    [in]  CORDB_ADDRESS    address,  
    [in]  ULONG32          bufsize,  
    [out, size_is(bufsize), length_is(*bufLen)]
        BYTE               buffer[],  
    [out] ULONG32          *bufLen  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `address`  
 から`CORDB_ADDRESS`ネイティブイメージオフセットを指定するオブジェクト。  
  
 `bufsize`  
 から配列のサイズ (バイト単位) `buffer` 。  
  
 `buffer`  
 入出力ブレークポイントによって置き換えられるオペコードを格納している配列。  
  
 `bufLen`  
 入出力配列で返されたバイト数へのポインター `buffer` 。  
  
## <a name="remarks"></a>Remarks  
 ネイティブイメージオフセットが共通言語ランタイム (CLR) 内にある場合、ブレークポイントは無視されます。 これにより、ブレークポイントがデバッガーによって設定されたときに、CLR は帯域外のブレークポイントのディスパッチを回避できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
