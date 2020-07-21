---
title: ICorDebugFrame::GetStackRange メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugFrame.GetStackRange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame::GetStackRange
helpviewer_keywords:
- GetStackRange method, ICorDebugFrame interface [.NET Framework debugging]
- ICorDebugFrame::GetStackRange method [.NET Framework debugging]
ms.assetid: fab037cb-fda6-40fb-9367-921e435dd5a0
topic_type:
- apiref
ms.openlocfilehash: cacdccf5c27cd1d115134d49e754b4ace2870b72
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205156"
---
# <a name="icordebugframegetstackrange-method"></a>ICorDebugFrame::GetStackRange メソッド
このスタックフレームの絶対アドレス範囲を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStackRange (  
    [out] CORDB_ADDRESS      *pStart,
    [out] CORDB_ADDRESS      *pEnd  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pStart`  
 入出力`CORDB_ADDRESS`このオブジェクトによって表されるスタックフレームの開始アドレスを指定するへのポインター `ICorDebugFrame` 。  
  
 `pEnd`  
 入出力`CORDB_ADDRESS`このオブジェクトによって表されるスタックフレームの終了アドレスを指定するへのポインター `ICorDebugFrame` 。  
  
## <a name="remarks"></a>Remarks  
 スタックのアドレス範囲は、複数のデバッグエンジンから収集されたインターリーブスタックトレースを piecing する場合に役立ちます。 数値の範囲は、スタックフレームの内容に関する情報を提供しません。 スタックフレームの位置を比較する場合にのみ意味があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
