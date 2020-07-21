---
title: ICorDebugThread3::GetActiveInternalFrames メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread3.GetActiveInternalFrames Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread3::GetActiveInternalFrames
helpviewer_keywords:
- ICorDebugThread3::GetActiveInternalFrames method [.NET Framework debugging]
- GetActiveInternalFrames method [.NET Framework debugging]
ms.assetid: d69796b4-5b6d-457c-85f6-2cf42e8a8773
topic_type:
- apiref
ms.openlocfilehash: 953b7c1cb5e471072776fe03e53a46d3ff19c0ac
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379862"
---
# <a name="icordebugthread3getactiveinternalframes-method"></a>ICorDebugThread3::GetActiveInternalFrames メソッド
スタック上の内部フレーム ([ICorDebugInternalFrame2](icordebuginternalframe2-interface.md) objects) の配列を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetActiveInternalFrames  
      (  
      [in] ULONG32 cInternalFrames,  
      [out] ULONG32 *pcInternalFrames,  
      [in, out,size_is(cInternalFrames), length_is(*pcInternalFrames)]  
            ICorDebugInternalFrame2 * ppInternalFrames[]  
      );  
```  
  
## <a name="parameters"></a>パラメーター  
 `cInternalFrames`  
 からで予期される内部フレームの数 `ppInternalFrames` 。  
  
 `pcInternalFrames`  
 入出力`ULONG32`スタック上の内部フレームの数を格納しているへのポインター。  
  
 `ppInternalFrames`  
 [入力、出力]スタック上の内部フレームの配列のアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|[ICorDebugInternalFrame2](icordebuginternalframe2-interface.md)オブジェクトが正常に作成されました。|  
|E_INVALIDARG|`cInternalFrames`が0では `ppInternalFrames` なく `null` 、がであるか、または `pcInternalFrames` がです `null` 。|  
|HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)|`ppInternalFrames`が内部フレームの数より小さくなっています。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>Remarks  
 内部フレームは、一時データを格納するためにランタイムによってスタックにプッシュされるデータ構造です。  
  
 を初めて呼び出すときは、 `GetActiveInternalFrames` パラメーターを `cInternalFrames` 0 (ゼロ) に設定し、パラメーターを null に設定する必要があり `ppInternalFrames` ます。 最初にが返されるときに `GetActiveInternalFrames` 、 `pcInternalFrames` スタック上の内部フレームの数を格納します。  
  
 `GetActiveInternalFrames`次に、を2回目に呼び出す必要があります。 パラメーターに適切なカウント () を渡し、 `pcInternalFrames` `cInternalFrames` で適切にサイズ設定された配列へのポインターを指定する必要があり `ppInternalFrames` ます。  
  
 実際のスタックフレームを返すには、の[テキスト](icordebugthread3-getactiveinternalframes-method.md)を使用します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
