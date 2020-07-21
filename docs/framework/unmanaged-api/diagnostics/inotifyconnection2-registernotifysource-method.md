---
title: INotifyConnection2::RegisterNotifySource メソッド
ms.date: 03/30/2017
api_name:
- INotifyConnection2.RegisterNotifySource
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifyConnection2::RegisterNotifySource
helpviewer_keywords:
- INotifyConnection2::RegisterNotifySource method [.NET Framework debugging]
- RegisterNotifySource method [.NET Framework debugging]
ms.assetid: 2632da80-6e4b-4429-8dee-b382745a5f81
topic_type:
- apiref
ms.openlocfilehash: b7fa777466e2c7edd7b3110dd91e776785c63c58
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442073"
---
# <a name="inotifyconnection2registernotifysource-method"></a>INotifyConnection2::RegisterNotifySource メソッド
指定された通知ソースをインストールします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RegisterNotifySource  
(  
    [in]  INotifySource2*  in_pNotifySource,  
    [out] INotifySink2**   out_ppNotifySink  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `in_pNotifySource`  
 から通知ソースとして使用するオブジェクトを指定します。  
  
 `out_ppNotifySink`  
 入出力通知シンクとして使用されるオブジェクトを受け取ります。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** ProtocolNotify2  
  
## <a name="see-also"></a>関連項目

- [INotifyConnection2 インターフェイス](inotifyconnection2-interface.md)
- [INotifySource2 インターフェイス](inotifysource2-interface.md)
- [INotifySink2 インターフェイス](inotifysink2-interface.md)
- [UnregisterNotifySource メソッド](inotifyconnection2-unregisternotifysource-method.md)
