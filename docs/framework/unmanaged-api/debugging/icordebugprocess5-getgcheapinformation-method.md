---
title: ICorDebugProcess5::GetGCHeapInformation メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.GetGCHeapInformation
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::GetGCHeapInformation
helpviewer_keywords:
- ICorDebugProcess5::GetGCHeapInformation method [.NET Framework debugging]
- GetGCHeapInformation method, ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: b9538ceb-230a-4079-9cb2-903dbf5c1848
topic_type:
- apiref
ms.openlocfilehash: 62d45da44a95eae399fbbd287aa997a5f913d0b0
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209657"
---
# <a name="icordebugprocess5getgcheapinformation-method"></a>ICorDebugProcess5::GetGCHeapInformation メソッド
現在列挙可能であるかどうかなど、ガベージコレクションヒープに関する一般的な情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetGCHeapInformation(  
    [out] COR_HEAPINFO *pHeapInfo  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pHeapInfo`  
 入出力ガベージコレクションヒープに関する全般的な情報を提供する[COR_HEAPINFO](cor-heapinfo-structure.md)値へのポインター。  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugProcess5::GetGCHeapInformation`プロセス内のガベージコレクション構造が現在有効であることを確認するには、ヒープまたは個々のヒープ領域を列挙する前に、メソッドを呼び出す必要があります。 コレクションの実行中にガベージコレクションヒープをウォークすることはできません。 それ以外の場合、列挙体は無効なガベージコレクション構造をキャプチャする可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess5 インターフェイス](icordebugprocess5-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
