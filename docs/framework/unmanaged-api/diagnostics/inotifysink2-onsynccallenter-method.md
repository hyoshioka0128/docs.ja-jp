---
title: INotifySink2::OnSyncCallEnter メソッド
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallEnter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallEnter
helpviewer_keywords:
- INotifySink2::OnSyncCallEnter method [.NET Framework debugging]
- OnSyncCallEnter method [.NET Framework debugging]
ms.assetid: e33265be-c25d-4145-ad02-c3e89d6f26c1
topic_type:
- apiref
ms.openlocfilehash: 85f00698f42f120b209cca14f293a58ae4c65f6f
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442034"
---
# <a name="inotifysink2onsynccallenter-method"></a>INotifySink2::OnSyncCallEnter メソッド
呼び出しを入力したときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnSyncCallEnter  
(  
    [in]  CALL_ID   in_CallID,  
    [in, size_is(in_BufferSize)] BYTE*  in_pBuffer,  
    [in]  DWORD     in_BufferSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `in_CallID`  
 から入力されている呼び出しの ID。 「 [CALL_ID 構造](call-id-structure.md)」を参照してください。  
  
 `in_pBuffer`  
 から呼び出しバッファー。  
  
 `in_BufferSize`  
 から呼び出しバッファーのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** ProtocolNotify2  
  
## <a name="see-also"></a>関連項目

- [INotifySink2 インターフェイス](inotifysink2-interface.md)
- [INotifySource2 インターフェイス](inotifysource2-interface.md)
- [INotifyConnection2 インターフェイス](inotifyconnection2-interface.md)
