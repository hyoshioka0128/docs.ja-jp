---
title: INotifySink2::OnSyncCallReturn メソッド
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallReturn
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallReturn
helpviewer_keywords:
- OnSyncCallReturn method [.NET Framework debugging]
- INotifySink2::OnSyncCallReturn method [.NET Framework debugging]
ms.assetid: c1bda761-6292-4750-a14b-7d5db8f33456
topic_type:
- apiref
ms.openlocfilehash: ff1dabcfc366607639cd98be4392f8dd59dc83a1
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442008"
---
# <a name="inotifysink2onsynccallreturn-method"></a>INotifySink2::OnSyncCallReturn メソッド
呼び出しから制御が戻ったときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnSyncCallReturn  
(  
    [in]  CALL_ID   in_CallID,  
    [in, size_is(in_BufferSize)] BYTE*  in_pBuffer,  
    [in]  DWORD     in_BufferSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `in_CallID`  
 からから返される呼び出しの ID。 「 [CALL_ID 構造](call-id-structure.md)」を参照してください。  
  
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
