---
title: ICorDebugProcess::ReadMemory メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ReadMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ReadMemory
helpviewer_keywords:
- ReadMemory method [.NET Framework debugging]
- ICorDebugProcess::ReadMemory method [.NET Framework debugging]
ms.assetid: 28e4b2f6-9589-445c-be24-24a3306795e7
topic_type:
- apiref
ms.openlocfilehash: ccd2350589126109ff11da439a8b83abfc4b91fa
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210476"
---
# <a name="icordebugprocessreadmemory-method"></a>ICorDebugProcess::ReadMemory メソッド
このプロセスの指定したメモリ領域を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ReadMemory(  
    [in]  CORDB_ADDRESS address,
    [in]  DWORD size,  
    [out, size_is(size), length_is(size)] BYTE buffer[],  
    [out] SIZE_T *read);  
```  
  
## <a name="parameters"></a>パラメーター  
 `address`  
 から`CORDB_ADDRESS`読み取るメモリのベースアドレスを指定する値。  
  
 `size`  
 からメモリから読み取るバイト数。  
  
 `buffer`  
 入出力メモリの内容を受け取るバッファー。  
  
 `read`  
 入出力指定したバッファーに転送されたバイト数へのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドは、主に、 `ReadMemory` デバッグ対象のアンマネージ部分で使用されているメモリ領域を検査するために相互運用機能デバッグによって使用されることを意図しています。 このメソッドを使用して、Microsoft 中間言語 (MSIL) コードとネイティブの JIT コンパイルコードを読み取ることもできます。  
  
 マネージブレークポイントは、パラメーターで返されたデータから削除され `buffer` ます。 [ICorDebugProcess2:: SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md)によって設定されたネイティブブレークポイントに対して調整は行われません。  
  
 プロセスメモリのキャッシュは実行されません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
