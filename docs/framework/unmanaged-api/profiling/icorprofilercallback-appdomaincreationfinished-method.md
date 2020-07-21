---
title: ICorProfilerCallback::AppDomainCreationFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainCreationFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainCreationFinished
helpviewer_keywords:
- AppDomainCreationFinished method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainCreationFinished method [.NET Framework profiling]
ms.assetid: dbab7d90-d515-4dc9-8195-294d5d04bab6
topic_type:
- apiref
ms.openlocfilehash: 76f56971223154d3ed966c272081049adf30de54
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500495"
---
# <a name="icorprofilercallbackappdomaincreationfinished-method"></a>ICorProfilerCallback::AppDomainCreationFinished メソッド
アプリケーションドメインが作成されたことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AppDomainCreationFinished(  
    [in] AppDomainID appDomainId,  
    [in] HRESULT     hrStatus);
```  
  
## <a name="parameters"></a>パラメーター

- `appDomainId`

  \[in] は、作成されたドメインを識別します。

- `hrStatus`

  \[in] アプリケーションドメインの作成が正常に完了したかどうかを示す HRESULT。

## <a name="remarks"></a>解説  
 アプリケーション ID は、メソッドが呼び出されるまで、情報要求に対して有効ではありません `AppDomainCreationFinished` 。  
  
 アプリケーションドメインの読み込みの一部は、コールバック後も続行される場合があり `AppDomainCreationFinished` ます。 のエラー HRESULT は `hrStatus` エラーを示します。 ただし、の成功 HRESULT は、 `hrStatus` アプリケーションドメインの作成の最初の部分が成功したことを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
