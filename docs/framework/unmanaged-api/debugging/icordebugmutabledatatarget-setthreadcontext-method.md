---
title: ICorDebugMutableDataTarget::SetThreadContext メソッド
ms.date: 03/30/2017
ms.assetid: 8c0d01d5-67e5-4522-9ccf-c8f3a78cb4fd
ms.openlocfilehash: a6df6bf030ad339f5d02b95cd191b30db60aa167
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210151"
---
# <a name="icordebugmutabledatatargetsetthreadcontext-method"></a>ICorDebugMutableDataTarget::SetThreadContext メソッド
スレッドのコンテキスト (レジスタの値) を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetThreadContext(  
   [in] DWORD dwThreadID,  
   [in] ULONG32 contextSize,   [in, size_is(contextSize)] const BYTE * pContext);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwThreadID`  
 [in] オペレーティング システム定義のスレッド識別子。  
  
 `contextSize`  
 [in]書き込まれる `pContext` バッファーのサイズ。  
  
 `pContext`  
 [in]書き込まれるバイト数へのポインター。  
  
## <a name="remarks"></a>Remarks  
 `SetThreadContext` メソッドは、オペレーティング システム定義の `dwThreadID` 引数で指定されるスレッドの現在のコンテキストを更新します。 コンテキストレコードの形式は、のプラットフォームによって決定されます。このプラットフォームでは、次[のように](icordebugdatatarget-getplatform-method.md)指定します。 Windows では、これは[コンテキスト](/windows/win32/api/winnt/ns-winnt-arm64_nt_context)構造です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugMutableDataTarget インターフェイス](icordebugmutabledatatarget-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
