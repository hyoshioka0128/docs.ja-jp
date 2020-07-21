---
title: ICorProfilerModuleEnum::Clone メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum.Clone Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum::Clone
helpviewer_keywords:
- Clone method, ICorProfilerModuleEnum interface [.NET Framework profiling]
- ICorProfilerModuleEnum::Clone method [.NET Framework profiling]
ms.assetid: 7dec7e36-8d88-416d-b437-abf98b76c1df
topic_type:
- apiref
ms.openlocfilehash: ccbb051ac30fb25199ce12c16fff74bb0b9944fa
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495087"
---
# <a name="icorprofilermoduleenumclone-method"></a>ICorProfilerModuleEnum::Clone メソッド
この[ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md)インターフェイスのコピーへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Clone([out] ICorProfilerObjectEnum **ppEnum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力次に、この[ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md)インターフェイスのコピーを指すインターフェイスポインターへのポインター。 列挙子のコピーは、この列挙子とは別に独自の列挙状態を保持します。 ただし、コピーの初期カーソル位置は、この列挙子の現在のカーソル位置と同じです。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerModuleEnum インターフェイス](icorprofilermoduleenum-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
