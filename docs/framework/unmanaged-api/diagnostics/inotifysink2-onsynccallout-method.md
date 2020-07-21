---
title: INotifySink2::OnSyncCallOut メソッド
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallOut
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallOut
helpviewer_keywords:
- INotifySink2::OnSyncCallOut method [.NET Framework debugging]
- OnSyncCallOut method [.NET Framework debugging]
ms.assetid: 97f15656-8677-4079-8553-a1d8603355d6
topic_type:
- apiref
ms.openlocfilehash: ce0e192a9d7d5abf56a55f844cf886c386f1c563
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441995"
---
# <a name="inotifysink2onsynccallout-method"></a>INotifySink2::OnSyncCallOut メソッド
呼び出しがタイムアウトしたときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnSyncCallOut  
(  
    [in]  CALL_ID  in_CallID,  
    [out, size_is(, *out_pBufferSize)] BYTE**  out_ppBuffer,  
    [out] DWORD*   out_pBufferSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `in_CallID`  
 から発信する呼び出しの ID。「 [CALL_ID 構造](call-id-structure.md)」を参照してください。  
  
 `out_ppBuffer`  
 入出力呼び出しバッファー。  
  
 `out_pBufferSize`  
 入出力呼び出しバッファーのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** ProtocolNotify2  
  
## <a name="see-also"></a>関連項目

- [INotifySink2 インターフェイス](inotifysink2-interface.md)
- [INotifySource2 インターフェイス](inotifysource2-interface.md)
- [INotifyConnection2 インターフェイス](inotifyconnection2-interface.md)
