---
title: ICorDebugStackWalk インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk
helpviewer_keywords:
- ICorDebugStackWalk interface [.NET Framework debugging]
ms.assetid: 16d695e8-975d-431b-8421-e9e6c3e3f476
topic_type:
- apiref
ms.openlocfilehash: 5f71dfcdffaaa683ca4f2abebaa99115ef90e0ff
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378907"
---
# <a name="icordebugstackwalk-interface"></a>ICorDebugStackWalk インターフェイス
スレッドのスタック上のマネージド メソッド (フレーム) を取得するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetContext メソッド](icordebugstackwalk-getcontext-method.md)|オブジェクト内の現在のフレームのコンテキストを返し `ICorDebugStackWalk` ます。|  
|[SetContext メソッド](icordebugstackwalk-setcontext-method.md)|`ICorDebugStackWalk`オブジェクトの現在のコンテキストをスレッドの有効なコンテキストに設定します。|  
|[Next メソッド](icordebugstackwalk-next-method.md)|オブジェクトを `ICorDebugStackWalk` 次のフレームに移動します。|  
|[GetFrame メソッド](icordebugstackwalk-getframe-method.md)|オブジェクト内の現在のフレームを取得し `ICorDebugStackWalk` ます。|  
  
## <a name="remarks"></a>Remarks  
  
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
