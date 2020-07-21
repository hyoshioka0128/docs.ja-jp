---
title: ICorDebugRegisterSet2::GetRegisters メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.GetRegisters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::GetRegisters
helpviewer_keywords:
- GetRegisters method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
- ICorDebugRegisterSet2::GetRegisters method [.NET Framework debugging]
ms.assetid: dbc498a8-ba3f-42f2-bdd9-b623c77a1019
topic_type:
- apiref
ms.openlocfilehash: 71b9d59621efb547713cb4a6c9df7a7142f4a677
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615190"
---
# <a name="icordebugregisterset2getregisters-method"></a>ICorDebugRegisterSet2:: GetRegisters メソッド

指定されたビットマスクによって指定された各レジスタの値を取得します (コードが現在実行されているプラットフォーム用)。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRegisters (  
    [in] ULONG32 maskCount,  
    [in, size_is(maskCount)] BYTE mask[],  
    [in] ULONG32 regCount,  
    [out, size_is(regCount)] CORDB_REGISTER regBuffer[]  
);  
```  
  
## <a name="parameters"></a>パラメーター

 `maskCount`  
 から配列のサイズ (バイト単位) `mask` 。  
  
 `mask`  
 からバイト配列。各ビットはレジスタに対応します。 ビットが1の場合は、対応するレジスタの値が取得されます。  
  
 `regCount`  
 から取得するレジスタ値の数。  
  
 `regBuffer`  
 入出力オブジェクトの配列 `CORDB_REGISTER` 。各オブジェクトは、レジスタの値を受け取ります。  
  
## <a name="remarks"></a>解説

 メソッドは、 `GetRegisters` マスクによって指定されたレジスタから値の配列を返します。 配列に、マスクビットが設定されていないレジスタの値が含まれていません。 したがって、配列のサイズは `regBuffer` マスク内の1の数と同じである必要があります。 の値 `regCount` がマスクで示されているレジスタの数に対して小さすぎる場合、番号が大きいレジスタの値はセットから切り捨てられます。 `regCount`が大きすぎる場合、未使用の `regBuffer` 要素は変更されません。  
  
 使用できないレジスタがマスクによって示されている場合、そのレジスタに対して不確定な値が返されます。  
  
 メソッドは、64を超える `ICorDebugRegisterSet2::GetRegisters` レジスタを持つプラットフォームに必要です。 たとえば、IA64 には128汎用レジスタと128浮動小数点レジスタがあるため、ビットマスクには64ビット以上が必要です。  
  
 X86 などのプラットフォームの場合と同様に、64以上のレジスタがない場合、メソッドは単にバイト配列のバイトをに変換し、次に、 `GetRegisters` `mask` `ULONG64` マスクを取得する[ICorDebugRegisterSet::GetRegisters](icordebugregisterset-getregisters-method.md) 、は、のようにします。 `ULONG64`  
  
## <a name="requirements"></a>要件

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugRegisterSet2 インターフェイス](icordebugregisterset2-interface.md)
- [ICorDebugRegisterSet インターフェイス](icordebugregisterset-interface.md)
