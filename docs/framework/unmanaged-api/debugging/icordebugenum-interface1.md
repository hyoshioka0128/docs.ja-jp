---
title: ICorDebugEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEnum
helpviewer_keywords:
- ICorDebugEnum interface [.NET Framework debugging]
ms.assetid: 80be7efe-2c32-4b9f-8c52-40c6f6268219
topic_type:
- apiref
ms.openlocfilehash: 7575be3f5074243b251c80b8dd5bdbb12e5d50fd
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976329"
---
# <a name="icordebugenum-interface"></a>ICorDebugEnum インターフェイス

デバッグアプリケーションで使用される列挙子の抽象基本インターフェイスとして機能します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Clone メソッド](icordebugenum-clone-method.md)|この `ICorDebugEnum` オブジェクトのコピーを作成します。|  
|[GetCount メソッド](icordebugenum-getcount-method.md)|列挙に含まれる項目の数を取得します。|  
|[Reset メソッド](icordebugenum-reset-method.md)|カーソルを列挙体の先頭に移動します。|  
|[Skip メソッド](icordebugenum-skip-method.md)|指定した数の項目だけ、列挙内でカーソルを前方に移動します。|  
  
## <a name="remarks"></a>Remarks  
 次の列挙子は`ICorDebugEnum`、から派生します。  
  
- ICorDebugAppDomainEnum  
  
- ICorDebugAssemblyEnum  
  
- [ICorDebugBlockingObjectEnum](icordebugblockingobjectenum-interface.md)  
  
- ICorDebugBreakpointEnum  
  
- ICorDebugChainEnum  
  
- ICorDebugCodeEnum  
  
- ICorDebugErrorInfoEnum  
  
- [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md)  
  
- ICorDebugFrameEnum  
  
- [ICorDebugGCReferenceEnum](icordebuggcreferenceenum-interface.md)  
  
- [ICorDebugGuidToTypeEnum](icordebugguidtotypeenum-interface.md)  
  
- [ICorDebugHeapEnum](icordebugheapenum-interface.md)  
  
- [ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md)  
  
- ICorDebugModuleEnum  
  
- ICorDebugObjectEnum  
  
- ICorDebugProcessEnum  
  
- ICorDebugStepperEnum  
  
- ICorDebugThreadEnum  
  
- ICorDebugTypeEnum  
  
- ICorDebugValueEnum  
  
- [ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md)  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
