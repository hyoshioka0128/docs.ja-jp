---
title: ICorDebugVariableHomeEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHomeEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHomeEnum
helpviewer_keywords:
- ICorDebugVariableHomeEnum interface [.NET Framework debugging]
ms.assetid: c312ae6d-c8dc-48d6-9f1e-ead515c88fdf
topic_type:
- apiref
ms.openlocfilehash: d5962de8cc2762f6ecf4864c5255da0fe83918e4
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396530"
---
# <a name="icordebugvariablehomeenum-interface"></a>ICorDebugVariableHomeEnum インターフェイス
関数のローカル変数および引数に列挙子を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Next メソッド](icordebugvariablehomeenum-next-method.md)|関数内のローカル変数および引数に関する情報を格納している指定された数の表示変数[home](icordebugvariablehome-interface.md)インスタンスを取得します。|  
  
## <a name="remarks"></a>解説  
 `ICorDebugVariableHomeEnum`インターフェイスは、ICorDebugEnum インターフェイスを実装します。  
  
 `ICorDebugVariableHomeEnum`インスタンスには、 [ICorDebugCode4:: EnumerateVariableHomes](icordebugcode4-enumeratevariablehomes-method.md)メソッドを呼び出すことによって、表示[変数 home](icordebugvariablehome-interface.md)インスタンスが設定されます。 コレクション内[の各は](icordebugvariablehome-interface.md)、関数のローカル変数または引数を表します。 コレクション内[のオブジェクトを](icordebugvariablehome-interface.md)列挙するには、[次](icordebugvariablehomeenum-next-method.md)のように指定します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugVariableHome インターフェイス](icordebugvariablehome-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
