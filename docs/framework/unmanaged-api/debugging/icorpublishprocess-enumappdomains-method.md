---
title: ICorPublishProcess::EnumAppDomains メソッド
ms.date: 03/30/2017
api_name:
- ICorPublishProcess.EnumAppDomains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcess::EnumAppDomains
helpviewer_keywords:
- EnumAppDomains method [.NET Framework debugging]
- ICorPublishProcess::EnumAppDomains method [.NET Framework debugging]
ms.assetid: 7da621fc-e7d0-4c00-9439-5c93619d7414
topic_type:
- apiref
ms.openlocfilehash: 0c3b5da52b78150198fa9f910bf01b4657e4eba8
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421164"
---
# <a name="icorpublishprocessenumappdomains-method"></a>ICorPublishProcess::EnumAppDomains メソッド
この[ICorPublishProcess](icorpublishprocess-interface.md)によって参照されるプロセス内のアプリケーションドメインの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumAppDomains (  
    [out] ICorPublishAppDomainEnum   **ppEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力このプロセス内のアプリケーションドメインのコレクションを反復処理できる[ICorPublishAppDomainEnum](icorpublishappdomainenum-interface.md)インスタンスのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 アプリケーションドメインの一覧は、メソッドが呼び出されたときに存在するアプリケーションドメインのスナップショットに基づいてい `EnumAppDomains` ます。 このメソッドは、新しい最新の一覧を作成するために複数回呼び出すことができます。 既存のリストは、このメソッドの後続の呼び出しの影響を受けません。  
  
 プロセスが終了した場合、 `EnumAppDomains` は CORDBG_E_PROCESS_TERMINATED の HRESULT 値で失敗します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublishProcess インターフェイス](icorpublishprocess-interface.md)
