---
title: ICorProfilerFunctionEnum::Clone メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum.Clone Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum::Clone
helpviewer_keywords:
- ICorProfilerFunctionEnum::Clone method [.NET Framework profiling]
- Clone method, ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 0c3d4835-e111-4e82-af6d-53f140b8f2c9
topic_type:
- apiref
ms.openlocfilehash: d6f348eb781efdef89926ec1bc267281bf3a5004
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503108"
---
# <a name="icorprofilerfunctionenumclone-method"></a>ICorProfilerFunctionEnum::Clone メソッド
この[ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md)インターフェイスのコピーへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Clone([out] ICorProfilerFunctionEnum **ppEnum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力インターフェイスポインターへのポインター。これにより、この[ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md)インターフェイスのコピーが参照されます。 列挙子のコピーは、この列挙子とは別に独自の列挙状態を保持します。 ただし、コピーの初期カーソル位置は、この列挙子の現在のカーソル位置と同じです。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerFunctionEnum インターフェイス](icorprofilerfunctionenum-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
