---
title: INotifyConnection2::UnregisterNotifySource メソッド
ms.date: 03/30/2017
api_name:
- INotifyConnection2.UnregisterNotifySource
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifyConnection2::UnregisterNotifySource
helpviewer_keywords:
- INotifyConnection2::UnregisterNotifySource method [.NET Framework debugging]
- UnregisterNotifySource method [.NET Framework debugging]
ms.assetid: 2fc6c715-646f-41fd-9c12-c59b40575269
topic_type:
- apiref
ms.openlocfilehash: 9d0fcdcd4fe1561f7565586e3327c6d3d7e0fe0a
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442047"
---
# <a name="inotifyconnection2unregisternotifysource-method"></a>INotifyConnection2::UnregisterNotifySource メソッド
指定された通知ソースオブジェクトを接続から削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UnregisterNotifySource  
(  
    [in]  INotifySource2*  in_pNotifySource  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `in_pNotifySource`  
 から登録を解除する通知オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** ProtocolNotify2  
  
## <a name="see-also"></a>関連項目

- [INotifyConnection2 インターフェイス](inotifyconnection2-interface.md)
- [INotifySource2 インターフェイス](inotifysource2-interface.md)
- [INotifySink2 インターフェイス](inotifysink2-interface.md)
- [RegisterNotifySource メソッド](inotifyconnection2-registernotifysource-method.md)
