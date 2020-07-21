---
title: ICorPublish::GetProcess メソッド
ms.date: 03/30/2017
api_name:
- ICorPublish.GetProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish::GetProcess
helpviewer_keywords:
- ICorPublish::GetProcess method [.NET Framework debugging]
- GetProcess method, ICorPublish interface [.NET Framework debugging]
ms.assetid: c5143805-2eb7-45b8-85ed-c8fb34df1084
topic_type:
- apiref
ms.openlocfilehash: 2cd2238ac67713564922be440ce64a2ebc4bbf44
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396330"
---
# <a name="icorpublishgetprocess-method"></a>ICorPublish::GetProcess メソッド
指定した識別子を持つプロセスを表す[ICorPublishProcess](icorpublishprocess-interface.md)インスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetProcess(  
    [in] unsigned              pid,
    [out] ICorPublishProcess   **ppProcess  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pid`  
 からプロセスの識別子。  
  
 `ppProcess`  
 入出力プロセスを表すインスタンスのアドレスへのポインター `ICorPublishProcess` 。  
  
## <a name="remarks"></a>解説  
 `GetProcess`プロセスが存在しない場合、または現在のユーザーがデバッグできるマネージプロセスでない場合は、失敗します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublish インターフェイス](icorpublish-interface.md)
