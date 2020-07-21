---
title: ICorProfilerCallback::ExceptionCLRCatcherFound メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionCLRCatcherFound
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionCLRCatcherFound
helpviewer_keywords:
- ICorProfilerCallback::ExceptionCLRCatcherFound method [.NET Framework profiling]
- ExceptionCLRCatcherFound method [.NET Framework profiling]
ms.assetid: 73fe8b4b-8f9a-4ba5-a10c-b26521396a66
topic_type:
- apiref
ms.openlocfilehash: 4f4d53b086453adce38902518f2de3dde1f2812f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500248"
---
# <a name="icorprofilercallbackexceptionclrcatcherfound-method"></a>ICorProfilerCallback::ExceptionCLRCatcherFound メソッド
`catch`例外のブロックが共通言語ランタイム (CLR) 自体で見つかった場合に呼び出されます。 このメソッドは .NET Framework バージョン2.0 では廃止されています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExceptionCLRCatcherFound();  
```  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 1.0  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ExceptionCLRCatcherExecute メソッド](icorprofilercallback-exceptionclrcatcherexecute-method.md)
