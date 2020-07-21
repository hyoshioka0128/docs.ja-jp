---
title: ICorDebugInternalFrame2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2
helpviewer_keywords:
- ICorDebugInternalFrame2 interface [.NET Framework debugging]
ms.assetid: d4755569-85b8-4ff4-bf50-0e608e76429f
topic_type:
- apiref
ms.openlocfilehash: ce3ca4745727a1738fdc1a526480d70ffc55ccf8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209904"
---
# <a name="icordebuginternalframe2-interface"></a>ICorDebugInternalFrame2 インターフェイス
内部フレームに関する情報を提供します。この情報には、スタック アドレス、および ICorDebugFrame オブジェクトを基準にした位置などが含まれます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetFrameAddress メソッド](icordebuginternalframe2-getframeaddress-method.md)|内部フレームのスタックアドレスを返します。|  
|[IsCloserToLeaf メソッド](icordebuginternalframe2-isclosertoleaf-method.md)|内部フレームが、指定されたのは、指定されたとしての `this` オブジェクトよりもリーフの近くにあるかどうかを確認します。|  
  
## <a name="remarks"></a>Remarks  
 このインターフェイスは、によって、、の各フレームインターフェイスを拡張します。  
  
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
