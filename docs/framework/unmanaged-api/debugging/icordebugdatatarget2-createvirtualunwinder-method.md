---
title: ICorDebugDataTarget2::CreateVirtualUnwinder メソッド
ms.date: 03/30/2017
ms.assetid: 354c8b4c-7d23-45c6-a7d7-3be4c2a5b772
ms.openlocfilehash: 7a479fba9bbcf28c60474fffc6219af23e62c251
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976500"
---
# <a name="icordebugdatatarget2createvirtualunwinder-method"></a>ICorDebugDataTarget2::CreateVirtualUnwinder メソッド
初期コンテキストからアンワインドを開始する新しいスタック アンワインダーを作成します (これは、必ずしもスレッドのリーフではありません)。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateVirtualUnwinder(  
    [in] DWORD nativeThreadID,  
    [in] ULONG32 contextFlags,  
    [in] ULONG32 cbContext,  
    [in, size_is(cbContext)] BYTE initialContext[],  
    [out] ICorDebugVirtualUnwinder ** ppUnwinder);  
};  
```  
  
## <a name="parameters"></a>パラメーター  
 nativeThreadID  
 [入力] スタックをアンワインドするスレッドのネイティブ スレッド ID。  
  
 contextFlags  
 [入力] コンテキストのどの部分が `initialContext` で定義されるかを指定するフラグ。  
  
 cbContext  
 [入力] `initialContext` のサイズ。  
  
 initialContext  
 [入力] コンテキストのデータ。  
  
 ppUnwinder  
 [出力] ICorDebugVirtualUnwinder インターフェイス オブジェクトのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 正常終了した場合は、`S_OK`。 それ以外の `HRESULT` は失敗を示します。 Mscordbi.dll に`HRESULT`よって受信された失敗は、致命的と見なさ`CORDBG_E_DATA_TARGET_ERROR`れ、 [ICorDebug](icordebug-interface.md)メソッドによって返されます。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugDataTarget2 インターフェイス](icordebugdatatarget2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
