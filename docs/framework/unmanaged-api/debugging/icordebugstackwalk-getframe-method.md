---
title: ICorDebugStackWalk::GetFrame メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.GetFrame Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::GetFrame
helpviewer_keywords:
- GetFrame method [.NET Framework debugging]
- ICorDebugStackWalk::GetFrame method [.NET Framework debugging]
ms.assetid: 4083b505-5b59-44fb-8c5d-129db6a96c10
topic_type:
- apiref
ms.openlocfilehash: 5f80125a67e634dda05b9427b5f46db8f21b29f8
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379210"
---
# <a name="icordebugstackwalkgetframe-method"></a>ICorDebugStackWalk::GetFrame メソッド
テキスト[オブジェクトの現在のフレーム](icordebugstackwalk-interface.md)を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFrame([out] ICorDebugFrame ** pFrame);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pFrame`  
 からスタック内の現在のフレームを表す、作成されたフレームオブジェクトのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|ランタイムは、現在のフレームを正常に返しました。|  
|E_FAIL|現在のフレームは返されませんでした。|  
|S_FALSE|現在のフレームはネイティブスタックフレームです。|  
|E_INVALIDARG|`pFrame` が null です。|  
|CORDBG_E_PAST_END_OF_STACK|フレームポインターは既にスタックの末尾にあります。そのため、追加のフレームにアクセスすることはできません。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugStackWalk`実際のスタックフレームだけを返します。 内部フレームを返すには、 [ICorDebugThread3:: GetActiveInternalFrames](icordebugthread3-getactiveinternalframes-method.md)メソッドを使用します。 内部フレームは、一時データを格納するためにランタイムによってスタックにプッシュされるデータ構造です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugStackWalk インターフェイス](icordebugstackwalk-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
