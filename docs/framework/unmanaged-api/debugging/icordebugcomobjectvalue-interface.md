---
title: ICorDebugComObjectValue のインターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugComObjectValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugComObjectValue
helpviewer_keywords:
- ICorDebugComObjectValue interface [.NET Framework debugging]
ms.assetid: 505a7f6c-d92b-42b4-b539-433f5102ea9b
topic_type:
- apiref
ms.openlocfilehash: 528db447df4d71d67441b05ad29e6a900c59afbb
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892823"
---
# <a name="icordebugcomobjectvalue-interface"></a>ICorDebugComObjectValue のインターフェイス
ランタイム呼び出し可能ラッパー (RCW) に関連付けられている情報を取得するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetCachedInterfacePointers メソッド](icordebugcomobjectvalue-getcachedinterfacepointers-method.md)|現在の RCW でキャッシュされている生のインターフェイスポインターを取得します。|  
|[GetCachedInterfaceTypes メソッド](icordebugcomobjectvalue-getcachedinterfacetypes-method.md)|現在のオブジェクトで使用または使用されているインターフェイス型の列挙子を提供します。|  
  
## <a name="remarks"></a>解説  
 "ICorDebugValue" インターフェイスのインスタンスが RCW を表すかどうかを確認するために`QueryInterface` 、デバッガーはを使用`IID_ICorDebugComObjectValue`して "icordebugvalue" でを呼び出します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
