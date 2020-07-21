---
title: ICorDebugFrame インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame
helpviewer_keywords:
- ICorDebugFrame interface [.NET Framework debugging]
ms.assetid: 0c48f764-3c64-4602-b2f4-4ffc60eb2c65
topic_type:
- apiref
ms.openlocfilehash: 9c2771d1338943406921447d96dd9a8748153a36
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209618"
---
# <a name="icordebugframe-interface"></a>ICorDebugFrame インターフェイス

現在のスタックのフレームを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateStepper メソッド](icordebugframe-createstepper-method.md)|このに対して相対的なステップ実行操作を実行する ICorDebugStepper を取得し `ICorDebugFrame` ます。|  
|[GetCallee メソッド](icordebugframe-getcallee-method.md)|このフレームが呼び出された現在のチェーン内のへのポインターを取得し `ICorDebugFrame` ます。または、このがチェーン内の最も内側のフレームである場合は null を返します。|  
|[GetCaller メソッド](icordebugframe-getcaller-method.md)|このフレームを呼び出した現在のチェーン内のへのポインターを取得し `ICorDebugFrame` ます。これがチェーンの最も外側のフレームである場合は null を返します。|  
|[GetChain メソッド](icordebugframe-getchain-method.md)|このが含まれている、ツールチェーンへのポインターを取得し `ICorDebugFrame` ます。|  
|[GetCode メソッド](icordebugframe-getcode-method.md)|このスタックフレームに関連付けられているテキストコードへのポインターを取得します。|  
|[GetFunction メソッド](icordebugframe-getfunction-method.md)|このスタックフレームに関連付けられているコードを格納しているコードを指すポインターを取得します。|  
|[GetFunctionToken メソッド](icordebugframe-getfunctiontoken-method.md)|このスタックフレームに関連付けられているコードを含む関数のメタデータトークンを取得します。|  
|[GetStackRange メソッド](icordebugframe-getstackrange-method.md)|このによって表されるスタックフレームの絶対アドレス範囲を取得し `ICorDebugFrame` ます。|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
