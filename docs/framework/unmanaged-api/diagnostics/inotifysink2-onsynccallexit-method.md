---
title: INotifySink2::OnSyncCallExit メソッド
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallExit
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallExit
helpviewer_keywords:
- INotifySink2::OnSyncCallExit method [.NET Framework debugging]
- OnSyncCallExit method [.NET Framework debugging]
ms.assetid: d9d7600e-a8f5-443a-96de-67d26e130f2d
topic_type:
- apiref
ms.openlocfilehash: f81ef3f5959e279b3fbbd94d6c5e8a2d86a38e7f
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442021"
---
# <a name="inotifysink2onsynccallexit-method"></a>INotifySink2::OnSyncCallExit メソッド
呼び出しを終了したときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnSyncCallExit  
(  
    [in]  CALL_ID   in_CallID,  
    [out, size_is(, *out_pBufferSize)] BYTE**  out_ppBuffer,  
    [out] DWORD*    out_pBufferSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `in_CallID`  
 から終了する呼び出しの ID。 「 [CALL_ID 構造](call-id-structure.md)」を参照してください。  
  
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
