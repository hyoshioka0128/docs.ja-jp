---
title: ICorProfilerCallback::ManagedToUnmanagedTransition メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ManagedToUnmanagedTransition
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ManagedToUnmanagedTransition
helpviewer_keywords:
- ManagedToUnmanagedTransition method [.NET Framework profiling]
- ICorProfilerCallback::ManagedToUnmanagedTransition method [.NET Framework profiling]
ms.assetid: ef3cd619-912d-40c5-a449-03ba02a39ee7
topic_type:
- apiref
ms.openlocfilehash: 9b53030fe860e02b0afd0dce3055ac3cf29e3491
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500001"
---
# <a name="icorprofilercallbackmanagedtounmanagedtransition-method"></a>ICorProfilerCallback::ManagedToUnmanagedTransition メソッド
マネージコードからアンマネージコードへの遷移が発生したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ManagedToUnmanagedTransition(  
    [in] FunctionID functionId,  
    [in] COR_PRF_TRANSITION_REASON reason);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionId`  
 から呼び出される関数の ID。  
  
 `reason`  
 からマネージコードからアンマネージコードへの呼び出しによって移行が発生したかどうか、またはアンマネージコードによって呼び出されたマネージ関数からの戻り値によって発生したものかどうかを示す[COR_PRF_TRANSITION_REASON](cor-prf-transition-reason-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>解説  
 の値 `reason` が COR_PRF_TRANSITION_CALL の場合、関数 ID はアンマネージ関数の ID であり、just-in-time コンパイラを使用してコンパイルされることはありません。 アンマネージ関数には、名前やメタデータなどの基本的な情報が関連付けられています。 アンマネージ関数が暗黙のプラットフォーム呼び出し (PInvoke) を使用して呼び出された場合、ランタイムは呼び出し先を特定できず、の値は null になり `functionId` ます。 暗黙の PInvoke の詳細については、「 [C++ Interop の使用 (暗黙的な pinvoke)](/cpp/dotnet/using-cpp-interop-implicit-pinvoke)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [UnmanagedToManagedTransition メソッド](icorprofilercallback-unmanagedtomanagedtransition-method.md)
- [C++ での明示的な PInvoke の使用 (DllImport 属性)](/cpp/dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute)
