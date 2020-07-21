---
title: ICorDebugRegisterSet::GetRegistersAvailable メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet.GetRegistersAvailable
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet::GetRegistersAvailable
helpviewer_keywords:
- ICorDebugRegisterSet::GetRegistersAvailable method [.NET Framework debugging]
- GetRegistersAvailable method, ICorDebugRegisterSet interface [.NET Framework debugging]
ms.assetid: 4ba08ffa-55a2-4662-9d6d-4738f1db60c9
topic_type:
- apiref
ms.openlocfilehash: 74eef0c1ec456d647e5a58e5009d2c77e5002289
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378290"
---
# <a name="icordebugregistersetgetregistersavailable-method"></a>ICorDebugRegisterSet::GetRegistersAvailable メソッド
[このは、この](icordebugregisterset-interface.md)"この" のどのレジスタが現在使用可能であるかを示すビットマスクを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRegistersAvailable (  
    [out] ULONG64   *pAvailable  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAvailable`  
 入出力現在使用できるレジスタを示すビットマスク。  
  
## <a name="remarks"></a>Remarks  
 特定の状況でその値を特定できない場合は、レジスタを使用できない可能性があります。  
  
 返されるマスクには、レジスタごとにビットが含まれています (1 << レジスタインデックス)。 レジスタが使用可能な場合、ビット値は1です。使用できない場合は0です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugRegisterSet インターフェイス](icordebugregisterset-interface.md)
- [ICorDebugRegisterSet2 インターフェイス](icordebugregisterset2-interface.md)
