---
title: ICorProfilerInfo5::SetEventMask2 メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- IcorProfilerInfo5.SetEventMask2
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 05dbbe2b-049c-4a60-be69-2ad7a949405e
topic_type:
- apiref
ms.openlocfilehash: 8027cdcde8281c363207e309bf65fcd90c03b626
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495620"
---
# <a name="icorprofilerinfo5seteventmask2-method"></a>ICorProfilerInfo5::SetEventMask2 メソッド
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 プロファイラーが共通言語ランタイム (CLR) からイベント通知を受け取ることを希望するイベントの型を指定する値を設定します。 [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)メソッドよりも多くの機能が用意されています。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetEventMask2(        [in] DWORD dwEventsLow,        [in] DWORD dwEventsHigh  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwEventsLow`  
 [in] イベントのカテゴリを指定する 4 バイトの値。 各ビットは、異なる性能、動作、またはイベントの型を制御します。 ビットは、 [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列挙体に記述されています。  
  
 `dwEventsHigh`  
 [in] イベントのカテゴリを指定する 4 バイトの値。  各ビットは、異なる性能、動作、またはイベントの型を制御します。 ビットは、 [COR_PRF_HIGH_MONITOR](cor-prf-high-monitor-enumeration.md)列挙体に記述されています。  
  
## <a name="remarks"></a>解説  
 `SetEventMask2` メソッドは、プロファイラーが登録するコールバックを設定するために使用します。 通常は、 [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md)メソッドを呼び出して、どのビットが設定されているかを判断し、その値と値および設定する新しいビットの論理 OR を実行 `pdwEventsLow` `pdwEventsHigh` してから、メソッドを呼び出し `SetEventMask2` ます。  
  
 このメソッドは、 [Seteventmask](icorprofilerinfo-seteventmask-method.md)メソッドの代替手段として推奨されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo5 インターフェイス](icorprofilerinfo5-interface.md)
- [GetEventMask2 メソッド](icorprofilerinfo5-geteventmask2-method.md)
