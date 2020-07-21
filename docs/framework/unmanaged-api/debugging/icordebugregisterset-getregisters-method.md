---
title: ICorDebugRegisterSet::GetRegisters メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet.GetRegisters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet::GetRegisters
helpviewer_keywords:
- GetRegisters method, ICorDebugRegisterSet interface [.NET Framework debugging]
- ICorDebugRegisterSet::GetRegisters method [.NET Framework debugging]
ms.assetid: fdf91864-48ea-4aa6-b70c-361b7a3184c7
topic_type:
- apiref
ms.openlocfilehash: 40de06d47654337542d2c80dc325f8201335312a
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379151"
---
# <a name="icordebugregistersetgetregisters-method"></a>ICorDebugRegisterSet::GetRegisters メソッド
ビットマスクによって指定された、(現在コードを実行しているコンピューター上の) 各レジスタの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRegisters (  
    [in] ULONG64       mask,
    [in] ULONG32       regCount,  
    [out, size_is(regCount), length_is(regCount)]  
        CORDB_REGISTER regBuffer[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mask`  
 から取得するレジスタ値を指定するビットマスク。 各ビットは、レジスタに対応します。 ビットが1に設定されている場合は、レジスタの値が取得されます。それ以外の場合は、レジスタの値は取得されません。  
  
 `regCount`  
 から取得するレジスタ値の数。  
  
 `regBuffer`  
 入出力オブジェクトの配列 `CORDB_REGISTER` 。各オブジェクトは、レジスタの値を受け取ります。  
  
## <a name="remarks"></a>Remarks  
 配列のサイズは、ビットマスクで1に設定されているビット数と同じである必要があります。 パラメーターは、 `regCount` レジスタ値を受け取るバッファー内の要素の数を指定します。 `regCount`マスクによって示されるレジスタの数に対して値が小さすぎる場合は、番号が大きいレジスタがセットから切り捨てられます。 `regCount`値が大きすぎる場合、未使用の `regBuffer` 要素は変更されません。  
  
 使用できないレジスタがビットマスクによって指定されている場合、は `GetRegisters` そのレジスタの不定値を返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugRegisterSet インターフェイス](icordebugregisterset-interface.md)
- [ICorDebugRegisterSet2 インターフェイス](icordebugregisterset2-interface.md)
