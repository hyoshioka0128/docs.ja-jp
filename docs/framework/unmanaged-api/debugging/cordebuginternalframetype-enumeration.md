---
title: CorDebugInternalFrameType 列挙型
ms.date: 03/30/2017
api_name:
- CorDebugInternalFrameType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugInternalFrameType
helpviewer_keywords:
- CorDebugInternalFrameType enumeration [.NET Framework debugging]
ms.assetid: e4412dc2-c338-4cfb-94d8-f682095dd2b1
topic_type:
- apiref
ms.openlocfilehash: 4a65a98ee04c3870dae2f49b3da2a8e72b1ffae4
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795834"
---
# <a name="cordebuginternalframetype-enumeration"></a>CorDebugInternalFrameType 列挙型
スタック フレームの型を示します。 この列挙体は、 [GetFrameType](icordebuginternalframe-getframetype-method.md)メソッドによって使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorDebugInternalFrameType {  
  
    STUBFRAME_NONE                 = 0x00000000,  
    STUBFRAME_M2U                  = 0x00000001,  
    STUBFRAME_U2M                  = 0x00000002,  
    STUBFRAME_APPDOMAIN_TRANSITION = 0x00000003,  
    STUBFRAME_LIGHTWEIGHT_FUNCTION = 0x00000004,  
    STUBFRAME_FUNC_EVAL            = 0x00000005,  
    STUBFRAME_INTERNALCALL         = 0x00000006,  
    STUBFRAME_CLASS_INIT           = 0x00000007,  
    STUBFRAME_EXCEPTION            = 0x00000008,  
    STUBFRAME_SECURITY             = 0x00000009,  
    STUBFRAME_JIT_COMPILATION     = 0x0000000a,  
} CorDebugInternalFrameType;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`STUBFRAME_NONE`|null 値です。 メソッド`ICorDebugInternalFrame::GetFrameType`は、この値を返しません。|  
|`STUBFRAME_M2U`|アンマネージスタブフレーム。|  
|`STUBFRAME_U2M`|アンマネージスタブフレーム。|  
|`STUBFRAME_APPDOMAIN_TRANSITION`|アプリケーションドメイン間の移行。|  
|`STUBFRAME_LIGHTWEIGHT_FUNCTION`|ライトウェイトメソッド呼び出し。|  
|`STUBFRAME_FUNC_EVAL`|関数の評価の開始。|  
|`STUBFRAME_INTERNALCALL`|共通言語ランタイムへの内部呼び出し。|  
|`STUBFRAME_CLASS_INIT`|クラスの初期化の開始。|  
|`STUBFRAME_EXCEPTION`|スローされる例外。|  
|`STUBFRAME_SECURITY`|コードアクセスセキュリティに使用されるフレーム。|  
|`STUBFRAME_JIT_COMPILATION`|ランタイムは、メソッドを JIT コンパイルしています。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
