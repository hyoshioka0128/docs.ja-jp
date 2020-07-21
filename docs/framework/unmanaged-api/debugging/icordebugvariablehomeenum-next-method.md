---
title: は、次のメソッドを実行します。
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHomeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHomeEnum::Next
helpviewer_keywords:
- ICorDebugVariableHomeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugVariableHomeEnum interface [.NET Framework debugging]
ms.assetid: eb9ea96c-5b58-4655-8104-094fc8b393b8
topic_type:
- apiref
ms.openlocfilehash: 980f563d3b11fbfcce48b6d7c05275af520e14f1
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396503"
---
# <a name="icordebugvariablehomeenumnext-method"></a>は、次のメソッドを実行します。
関数内のローカル変数および引数に関する情報を格納している指定された数の表示変数[home](icordebugvariablehome-interface.md)インスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)] ICorDebugVariableHome *homes[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 [in] 取得するオブジェクトの数。  
  
 `homes`  
 ポインターの配列。各ポインターは、関数のローカル変数または引数に関する情報を提供[する、の各オブジェクトを](icordebugvariablehome-interface.md)参照します。  
  
 `pceltFetched`  
 入出力実際にオブジェクトで返されたインスタンスの数。  
  
## <a name="return-value"></a>戻り値  
 メソッドは、次の値を返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|メソッドは正常に完了しました。|  
|`S_FALSE`|に反映された実際のインスタンス数 `pceltFetched` が、要求されたインスタンスの数より少なくなっています。|  
  
## <a name="remarks"></a>解説  
 [次](icordebugvariablehomeenum-next-method.md)のメソッドは、 `celt` 列挙子の現在位置を起点として、最大オブジェクトを取得します。 メソッドから制御が戻るときに、 `pceltFetched` 取得したオブジェクトの実際の数を格納します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugVariableHomeEnum インターフェイス](icordebugvariablehomeenum-interface.md)
- [ICorDebugVariableHome インターフェイス](icordebugvariablehome-interface.md)
