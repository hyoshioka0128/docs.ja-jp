---
title: ICorProfilerCallback::UnmanagedToManagedTransition メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.UnmanagedToManagedTransition
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition
helpviewer_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition method [.NET Framework profiling]
- UnmanagedToManagedTransition method [.NET Framework profiling]
ms.assetid: ade2cc01-9b81-4e09-a5f9-b3b9dda27e96
topic_type:
- apiref
ms.openlocfilehash: 8734fa9c9418b818cbe14ebe87ce2af6fa59c078
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499845"
---
# <a name="icorprofilercallbackunmanagedtomanagedtransition-method"></a>ICorProfilerCallback::UnmanagedToManagedTransition メソッド
アンマネージコードからマネージコードへの遷移が発生したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UnmanagedToManagedTransition(  
    [in] FunctionID functionId,  
    [in] COR_PRF_TRANSITION_REASON reason);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionId`  
 から呼び出される関数の ID。  
  
 `reason`  
 からアンマネージコードからのマネージコードの呼び出しによって移行が発生したかどうか、またはマネージ関数によって呼び出されたアンマネージ関数からの戻りが原因で発生したかどうかを示す[COR_PRF_TRANSITION_REASON](cor-prf-transition-reason-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>解説  
 の値 `reason` が COR_PRF_TRANSITION_RETURN であり、 `functionId` が null でない場合、関数 ID はアンマネージ関数の ID であり、JUST-IN-TIME (JIT) コンパイラを使用してコンパイルされることはありません。 アンマネージ関数には、名前やメタデータなど、いくつかの基本的な情報が関連付けられています。  
  
 の値が COR_PRF_TRANSITION_CALL 場合は、呼び出された `reason` 関数 (つまり、マネージ関数) がまだ JIT でコンパイルされていない可能性があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ManagedToUnmanagedTransition メソッド](icorprofilercallback-managedtounmanagedtransition-method.md)
- [C++ での明示的な PInvoke の使用 (DllImport 属性)](/cpp/dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute)
- [C++ Interop (暗黙の PInvoke) の使用](/cpp/dotnet/using-cpp-interop-implicit-pinvoke)
