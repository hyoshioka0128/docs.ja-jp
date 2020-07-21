---
title: CorDebugExceptionObjectStackFrame 構造体
ms.date: 03/30/2017
api_name:
- CorDebugExceptionObjectStackFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugExceptionObjectStackFrame
helpviewer_keywords:
- CorDebugExceptionObjectStackFrame structure [.NET Framework debugging]
ms.assetid: 542cdd81-5ae7-4361-b0ef-1ae4775df258
topic_type:
- apiref
ms.openlocfilehash: 7eccaf984b187e463195bb3804f87bbb2c7ad47b
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795925"
---
# <a name="cordebugexceptionobjectstackframe-structure"></a>CorDebugExceptionObjectStackFrame 構造体
例外オブジェクトのスタック フレームの情報を表しています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct CorDebugExceptionObjectStackFrame {  
    ICorDebugModule* pModule;  
    CORDB_ADDRESS ip;  
    mdMethodDef methodDef;  
    BOOL isLastForeignExceptionFrame;  
} CorDebugExceptionObjectStackFrame;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`pModule`|現在のフレームのモジュールオブジェクトへのポインター。|  
|`ip`|現在のフレームの命令ポインター (EIP/RIP) の値。|  
|`methodDef`|現在のフレームのメソッドトークン。|  
|`isLastForeignExceptionFrame`|フレームが外部例外の最後のフレームであるかどうかを示す値。|  
  
## <a name="remarks"></a>Remarks  
 呼び出し元は、使用されなくなったときに、モジュールオブジェクトへのポインターを解放する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
