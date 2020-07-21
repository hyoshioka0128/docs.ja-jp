---
title: ICorDebugThread4::GetBlockingObjects メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread4.GetBlockingObjects Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread4::GetBlockingObjects
helpviewer_keywords:
- GetBlockingObjects method [.NET Framework debugging]
- ICorDebugThread4::GetBlockingObjects method [.NET Framework debugging]
ms.assetid: a7e6c54e-7be9-4e52-bbb4-95f52458e8e4
topic_type:
- apiref
ms.openlocfilehash: 366b5124cc66a4e9a1c3bd4e77f604f15ba8d8a8
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379681"
---
# <a name="icordebugthread4getblockingobjects-method"></a>ICorDebugThread4::GetBlockingObjects メソッド
スレッドブロック情報を提供する[CorDebugBlockingObject](cordebugblockingobject-structure.md)構造体の順序付けられた列挙体を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetBlockingObjects (  
    [out] ICorDebugBlockingObjectEnum **ppBlockingObjectEnum  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppBlockingObjectEnum`  
 入出力[CorDebugBlockingObject](cordebugblockingobject-structure.md)構造体の順序付けられた列挙体へのポインター。  
  
## <a name="remarks"></a>Remarks  
 返された列挙体の最初の要素は、スレッドをブロックしている最初の構造体に対応します。 2番目の要素は、非同期プロシージャ呼び出し (APC) の実行中に検出されるブロッキング項目に対応します。  
  
 列挙は、現在の同期済みの状態の間のみ有効です。  
  
 このメソッドは、デバッグ対象が synchronized 状態のときに呼び出す必要があります。  
  
 `ppBlockingObjectEnum`が有効なポインターでない場合、結果は未定義になります。  
  
 スレッドがブロックされていて、エラーを特定できない場合、メソッドは失敗を示す HRESULT を返します。それ以外の場合は S_OK を返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugThread4 インターフェイス](icordebugthread4-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
