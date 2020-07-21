---
title: ICorProfilerInfo::ForceGC メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.ForceGC
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::ForceGC
helpviewer_keywords:
- ICorProfilerInfo::ForceGC method [.NET Framework profiling]
- ForceGC method [.NET Framework profiling]
ms.assetid: 0da1ef80-d242-4636-87d0-43e0470b342a
topic_type:
- apiref
ms.openlocfilehash: 9bc6619f3ef383c7bf60a310a87f056cfc43cddf
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498675"
---
# <a name="icorprofilerinfoforcegc-method"></a>ICorProfilerInfo::ForceGC メソッド
共通言語ランタイム (CLR) 内で強制的にガベージコレクションを実行します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ForceGC();  
```  
  
## <a name="remarks"></a>解説  
 メソッドを呼び出す必要があるのは、 `ForceGC` マネージコードを実行しておらず、そのスタックにプロファイラーコールバックがないスレッドだけです。 最も便利な実装は、 `ForceGC` シグナル状態になったときにを呼び出す、プロファイラー内に個別のスレッドを作成することです。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
