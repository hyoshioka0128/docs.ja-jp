---
title: ICorDebugStackWalk::GetContext メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.GetContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::GetContext
helpviewer_keywords:
- GetContext method, ICorDebugStackWalk interface [.NET Framework debugging]
- ICorDebugStackWalk::GetContext method [.NET Framework debugging]
ms.assetid: 081d1c95-152b-4797-8552-18453eb7b14b
topic_type:
- apiref
ms.openlocfilehash: 743b0c8016ca5c0401046166a770d857215429a3
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379213"
---
# <a name="icordebugstackwalkgetcontext-method"></a>ICorDebugStackWalk::GetContext メソッド
[は、テキストオブジェクト内](icordebugstackwalk-interface.md)の現在のフレームのコンテキストを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetContext([in]  ULONG32 contextFlags,  
                   [in]  ULONG32 contextBufSize,  
                   [out] ULONG32* contextSize,  
                   [out, size_is(contextBufSize)] BYTE contextBuf[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `contextFlags`  
 からコンテキストバッファーの要求されたコンテンツを示すフラグ (Winnt.h で定義されています)。  
  
 `contextBufSize`  
 からコンテキストバッファーに割り当てられたサイズ。  
  
 `contextSize`  
 入出力コンテキストの実際のサイズ。 この値は、コンテキストバッファーのサイズ以下である必要があります。  
  
 `contextBuf`  
 入出力コンテキストバッファー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|現在のフレームのコンテキストが正常に返されました。|  
|E_FAIL|コンテキストを返すことができませんでした。|  
|HRESULT_FROM_WIN32 (ERROR_INSUFFICIENT バッファー)|コンテキストバッファーが小さすぎます。|  
|CORDBG_E_PAST_END_OF_STACK|フレームポインターは既にスタックの末尾にあります。そのため、追加のフレームにアクセスすることはできません。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>Remarks  
 アンワインドでは、非揮発性レジスタなどのレジスタのサブセットのみが復元されるため、呼び出し時にコンテキストがレジスタの状態と完全に一致するとは限りません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
