---
title: ICorDebugProcess5::EnumerateHeap メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeap
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeap
helpviewer_keywords:
- EnumerateHeap method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeap method [.NET Framework debugging]
ms.assetid: b0192104-6073-4089-a4df-dc29ee033074
topic_type:
- apiref
ms.openlocfilehash: 9386c77cc98df17d797d5886e1603ffc4824b6dc
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205233"
---
# <a name="icordebugprocess5enumerateheap-method"></a>ICorDebugProcess5::EnumerateHeap メソッド
マネージヒープ上のオブジェクトの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateHeap(  
    [out] ICorDebugHeapEnum **ppObjects  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppObject`  
 入出力マネージヒープ上に存在するオブジェクト[の列挙子](icordebugheapenum-interface.md)である、コードオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドを呼び出す前に `ICorDebugProcess5::EnumerateHeap` 、 [ICorDebugProcess5:: Getg](icordebugprocess5-getgcheapinformation-method.md)メソッドを呼び出し、 `areGCStructuresValid` 返された[COR_HEAPINFO](cor-heapinfo-structure.md)オブジェクトのフィールドの値を調べて、現在の状態のガベージコレクションヒープが列挙可能であることを確認する必要があります。 さらに、は `ICorDebugProcess5::EnumerateHeap` 、 `E_FAIL` プロセスの有効期間が早すぎると、マネージヒープのメモリが割り当てられる前に、を返します。  
  
 は[、ICorDebugEnum](icordebugheapenum-interface.md)インターフェイスから派生した標準列挙子であり、 [COR_HEAPOBJECT](cor-heapobject-structure.md)オブジェクトを列挙できます。 このメソッド[は、すべてのオブジェクト](icordebugheapenum-interface.md)に関する情報を提供する[COR_HEAPOBJECT](cor-heapobject-structure.md)インスタンスを使用して、このコレクションオブジェクトを設定します。 コレクションには、オブジェクトによってルートされていないが、まだガベージコレクターによって収集されていないオブジェクトに関する情報を提供する[COR_HEAPOBJECT](cor-heapobject-structure.md)インスタンスを含めることもできます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess5 インターフェイス](icordebugprocess5-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
