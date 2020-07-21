---
title: ICorDebugThread3 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugThread3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread3
helpviewer_keywords:
- ICorDebugThread3 interface [.NET Framework debugging]
ms.assetid: eb2860ef-06cb-4968-a6c3-6d048ecda2a4
topic_type:
- apiref
ms.openlocfilehash: dc556dfb59e999ed9b7fc5f35c603dc26c35f314
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378706"
---
# <a name="icordebugthread3-interface"></a>ICorDebugThread3 インターフェイス
とそれに対応するインターフェイス[へのエントリ](icordebugstackwalk-interface.md)ポイントを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateStackWalk メソッド](icordebugthread3-createstackwalk-method.md)|スタックをアンワインドするスレッドに対し[て、このオブジェクトを](icordebugstackwalk-interface.md)作成します。|  
|[GetActiveInternalFrames メソッド](icordebugthread3-getactiveinternalframes-method.md)|スタック上の内部フレーム ([ICorDebugInternalFrame2](icordebuginternalframe2-interface.md) objects) の配列を返します。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugThread3`は、のように、の論理上の拡張機能です。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
