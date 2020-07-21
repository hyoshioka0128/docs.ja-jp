---
title: ICorDebugVariableHome インターフェイス
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugVariableHome
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome
helpviewer_keywords:
- ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: 76f2bf3b-759f-4eed-bce7-119415b25915
topic_type:
- apiref
ms.openlocfilehash: caf6a24207be98be9afb10be2bd027b51405fa3b
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396545"
---
# <a name="icordebugvariablehome-interface"></a>ICorDebugVariableHome インターフェイス
関数のローカル変数または引数を表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetArgumentIndex メソッド](icordebugvariablehome-getargumentindex-method.md)|関数の引数のインデックスを取得します。|  
|[GetCode メソッド](icordebugvariablehome-getcode-method.md)|このオブジェクトを含む "コード" インスタンスを取得し `ICorDebugVariableHome` ます。|  
|[GetLiveRange メソッド](icordebugvariablehome-getliverange-method.md)|この変数がライブであるネイティブ範囲を取得します。|  
|[GetLocationType メソッド](icordebugvariablehome-getlocationtype-method.md)|変数のネイティブな場所の型を取得します。|  
|[GetOffset メソッド](icordebugvariablehome-getoffset-method.md)|変数の基本レジスタからのオフセットを取得します。|  
|[GetRegister メソッド](icordebugvariablehome-getregister-method.md)|の場所の種類がである変数 `VLT_REGISTER` と、の場所の種類がの変数の基本レジスタを含むレジスタを取得し `VLT_REGISTER_RELATIVE` ます。|  
|[GetSlotIndex メソッド](icordebugvariablehome-getslotindex-method.md)|ローカル変数のマネージドスロットインデックスを取得します。|  
  
## <a name="example"></a>例  
 次のコード片では、という名前の[ICorDebugCode4](icordebugcode4-interface.md)オブジェクトを使用し `pCode4` ます。  
  
```cpp  
ICorDebugCode4 *pCode4 = NULL;  
pCode->QueryInterface(IID_ICorDebugCode4, &pCode4);  
  
ICorDebugVariableEnum *pVarLocEnum = NULL;  
pCode4->EnumerateVariableHomes(&pVarLocEnum);  
  
// retrieve local variables and arguments  
ULONG celt = 0;  
pVarLocEnum->GetCount(&celt);  
ICorDebugVariableHome **homes = new ICorDebugVariableHome *[celt];  
ULONG celtFetched = 0;  
pVarLocEnum->Next(celt, homes, &celtFetched);  
  
for (int i = 0; i < celtFetched; i++)  
{  
    VariableLocationType locType = VLT_INVALID;  
    homes[i].GetLocationType(&locType);  
    switch (locType)  
    {  
    case VLT_REGISTER:  
        CorDebugRegister register = 0;  
        locals[i].GetRegister(&register);  
        // now we know which register it is in  
        break;  
    case VLT_REGISTER_RELATIVE:  
        CorDebugRegister baseRegister = 0;  
        LONG offset = 0;  
        locals[i].GetRegister(&register);  
        locals[i].GetOffset(&offset);  
        // now we know the register-relative offset  
        break;  
    case VLT_INVALID:  
        // handle case where we can't access the location  
        break;  
    }  
}  
```  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [ICorDebugVariableHomeEnum インターフェイス](icordebugvariablehomeenum-interface.md)
