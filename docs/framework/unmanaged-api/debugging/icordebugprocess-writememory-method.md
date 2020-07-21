---
title: ICorDebugProcess::WriteMemory メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.WriteMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::WriteMemory
helpviewer_keywords:
- ICorDebugProcess::WriteMemory method [.NET Framework debugging]
- WriteMemory method [.NET Framework debugging]
ms.assetid: d5c07d86-045d-4391-893b-0bcd2959f90e
topic_type:
- apiref
ms.openlocfilehash: 0a433ccb81ef62ac92a4553a838a2c98a04fc7c1
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212816"
---
# <a name="icordebugprocesswritememory-method"></a>ICorDebugProcess::WriteMemory メソッド
このプロセスのメモリ領域にデータを書き込みます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT WriteMemory(  
    [in]  CORDB_ADDRESS address,  
    [in]  DWORD size,  
    [in, size_is(size)] BYTE buffer[],  
    [out] SIZE_T *written);  
```  
  
## <a name="parameters"></a>パラメーター  
 `address`  
 から`CORDB_ADDRESS`データが書き込まれるメモリ領域のベースアドレスを表す値。 データ転送が行われる前に、システムは、ベースアドレスを開始位置として、指定したサイズのメモリ領域が書き込み可能であることを確認します。 アクセスできない場合、メソッドは失敗します。  
  
 `size`  
 からメモリ領域に書き込まれるバイト数。  
  
 `buffer`  
 から書き込むデータを格納するバッファー。  
  
 `written`  
 入出力このプロセスのメモリ領域に書き込まれたバイト数を受け取る変数へのポインター。 `written`が NULL の場合、このパラメーターは無視されます。  
  
## <a name="remarks"></a>Remarks  
 データは、ブレークポイントの背後に自動的に書き込まれます。 .NET Framework バージョン2.0 では、ネイティブデバッガーは、このメソッドを使用して命令ストリームにブレークポイントを挿入することはできません。 代わりに[ICorDebugProcess2:: SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md)を使用してください。  
  
 メソッドは、 `WriteMemory` マネージコードの外部でのみ使用する必要があります。 不適切に使用された場合、このメソッドはランタイムを破損する可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
