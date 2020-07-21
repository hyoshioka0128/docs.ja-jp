---
title: ICorProfilerCallback::AppDomainShutdownFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainShutdownFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainShutdownFinished
helpviewer_keywords:
- AppDomainShutdownFinished method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainShutdownFinished method [.NET Framework profiling]
ms.assetid: 52794819-0a59-4bb1-a265-0f158cd5cd65
topic_type:
- apiref
ms.openlocfilehash: 722a1e0adea41a13ca25829c53372c29187b80bd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500469"
---
# <a name="icorprofilercallbackappdomainshutdownfinished-method"></a>ICorProfilerCallback::AppDomainShutdownFinished メソッド
アプリケーションドメインがプロセスからアンロードされたことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AppDomainShutdownFinished(  
    [in] AppDomainID appDomainId,  
    [in] HRESULT     hrStatus);  
```  
  
## <a name="parameters"></a>パラメーター

- `appDomainId`

  \[in] は、アプリケーションのアセンブリが格納されているドメインを識別します。

- `hrStatus`

  \[in] アプリケーションドメインが正常にアンロードされたかどうかを示す HRESULT。

## <a name="remarks"></a>解説  
 `appDomainId` [ICorProfilerCallback:: AppDomainShutdownStarted](icorprofilercallback-appdomainshutdownstarted-method.md)メソッドがを返すと、の値は情報要求に対して有効ではありません。  
  
 アプリケーションドメインのアンロードの一部は、コールバック後に続行される場合があり `AppDomainCreationFinished` ます。 のエラー HRESULT は `hrStatus` エラーを示します。 ただし、の成功 HRESULT は、 `hrStatus` アプリケーションドメインのアンロードの最初の部分が成功したことを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
