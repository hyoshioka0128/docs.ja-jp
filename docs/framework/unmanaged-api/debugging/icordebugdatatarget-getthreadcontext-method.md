---
title: ICorDebugDataTarget::GetThreadContext メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.GetThreadContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::GetThreadContext
helpviewer_keywords:
- ICorDebugDataTarget::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: c8954268-1821-4b23-b665-dbb55f2af31b
topic_type:
- apiref
ms.openlocfilehash: 79708aa5a2abcb8d7465f82a8beb918484c193b9
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976552"
---
# <a name="icordebugdatatargetgetthreadcontext-method"></a>ICorDebugDataTarget::GetThreadContext メソッド
指定されたスレッドの現在のスレッドコンテキストを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetThreadContext(  
       [in] DWORD dwThreadID,  
       [in] ULONG32 contextFlags,  
       [in] ULONG32 contextSize,  
       [out, size_is(contextSize)] BYTE * pContext);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwThreadID`  
 からコンテキストを取得するスレッドの識別子。 識別子はオペレーティングシステムによって定義されます。  
  
 `contextFlags`  
 からコンテキストのどの部分を読み取る必要があるかを示す、プラットフォームに依存するフラグのビットごとの組み合わせ。  
  
 `contextSize`  
 [入力] `pContext` のサイズ。  
  
 `pContext`  
 入出力スレッドコンテキストが格納されるバッファー。  
  
## <a name="remarks"></a>Remarks  
 Windows プラットフォームでは`pContext` 、は、 `CONTEXT`の構造体 (winnt.h で定義されています) である必要があります。これは[、の型](icordebugdatatarget-getplatform-method.md)によって指定されたコンピューターの種類に適しています。 `contextFlags``CONTEXT`構造体の`ContextFlags`フィールドと同じ値を持つ必要があります。 `CONTEXT`構造体はプロセッサ固有です。詳細については、「Winnt.h ファイル」を参照してください。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugDataTarget インターフェイス](icordebugdatatarget-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
