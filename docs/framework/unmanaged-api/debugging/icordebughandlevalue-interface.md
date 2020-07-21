---
title: ICorDebugHandleValue インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugHandleValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHandleValue
helpviewer_keywords:
- ICorDebugHandleValue interface [.NET Framework debugging]
ms.assetid: 66fcd2b8-ac66-414b-83a8-75a925e17772
topic_type:
- apiref
ms.openlocfilehash: c901e21521e941c51939958175a5316808890e9f
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83208617"
---
# <a name="icordebughandlevalue-interface"></a>ICorDebugHandleValue インターフェイス

デバッガーがガベージコレクションのハンドルを作成した参照値を表す、値のサブクラス。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Dispose メソッド](icordebughandlevalue-dispose-method.md)|`ICorDebugHandleValue`インターフェイスポインターを明示的に解放せずに、このオブジェクトによって参照されるハンドルを解放します。|  
|[GetHandleType メソッド](icordebughandlevalue-gethandletype-method.md)|このによって参照されるハンドルの種類を記述する CorDebugHandleType 値を取得し `ICorDebugHandleValue` ます。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugReferenceValue`デバッグ対象のコードの実行が中断された場合、オブジェクトは無効になります。 は、 `ICorDebugHandleValue` 明示的に解放されるまで、中断および継続による参照を保持します。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
