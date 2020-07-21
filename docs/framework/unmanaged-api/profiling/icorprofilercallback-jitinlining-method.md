---
title: ICorProfilerCallback::JITInlining メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITInlining
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITInlining
helpviewer_keywords:
- JITInlining method [.NET Framework profiling]
- ICorProfilerCallback::JITInlining method [.NET Framework profiling]
ms.assetid: c2f45801-dd38-4b78-b6b7-64397dc73f83
topic_type:
- apiref
ms.openlocfilehash: 13ce44c9c7a04b870278bc8926dd9fe5daf10bc3
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500014"
---
# <a name="icorprofilercallbackjitinlining-method"></a>ICorProfilerCallback::JITInlining メソッド
Just-in-time (JIT) コンパイラが、別の関数と共に関数を挿入しようとしていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT JITInlining(  
    [in]  FunctionID callerId,  
    [in]  FunctionID calleeId,  
    [out] BOOL      *pfShouldInline);  
```  
  
## <a name="parameters"></a>パラメーター  
 `callerId`  
 から関数が挿入される関数の ID `calleeId` 。  
  
 `calleeId`  
 から挿入する関数の ID。  
  
 `pfShouldInline`  
 [出力] `true`挿入の実行を許可する場合は。それ以外の場合は `false` 。  
  
## <a name="remarks"></a>解説  
 プロファイラーでをに設定すると、関数が `pfShouldInline` `false` `calleeId` 関数に挿入されないようにすることができ `callerId` ます。 また、プロファイラーは、 [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列挙体の COR_PRF_DISABLE_INLINING 値を使用して、インライン挿入をグローバルに無効にすることができます。  
  
 インラインで挿入された関数は、入力または終了するためのイベントを発生させません。 したがって、 `pfShouldInline` 正確なコールグラフを生成するためには、プロファイラーをに設定する必要があり `false` ます。 `pfShouldInline`をに設定する `false` と、パフォーマンスに影響します。インライン挿入では通常、速度が向上し、挿入されたメソッドの個別の JIT コンパイルイベントの数が減少するためです。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
