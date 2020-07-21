---
title: ICorConfiguration::AddDebuggerSpecialThread メソッド
ms.date: 03/30/2017
api_name:
- ICorConfiguration.AddDebuggerSpecialThread
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- AddDebuggerSpecialThread
helpviewer_keywords:
- AddDebuggerSpecialThread method [.NET Framework hosting]
- ICorConfiguration::AddDebuggerSpecialThread method [.NET Framework hosting]
ms.assetid: 1f1e3239-438e-4be9-a3bb-7d0722d3a76d
topic_type:
- apiref
ms.openlocfilehash: 8b6593ad995872f0e0014b1e8bcd8a4b576bbeaf
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762430"
---
# <a name="icorconfigurationadddebuggerspecialthread-method"></a>ICorConfiguration::AddDebuggerSpecialThread メソッド
デバッグサービスに対して、マネージまたはアンマネージのデバッグシナリオでデバッガーがアプリケーションを停止している間に、特定のスレッドの実行を継続できるようにする必要があることを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AddDebuggerSpecialThread (  
    [in] DWORD dwSpecialThreadId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwSpecialThreadId`  
 から実行を継続することが許可されているスレッドの ID。  
  
## <a name="remarks"></a>解説  
 指定されたスレッドはマネージコードの実行を許可されないか、または任意の方法でランタイムに入ることができません。 このようなスレッドの例として、レガシスクリプトデバッガーをサポートするインプロセススレッドがあります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorConfiguration インターフェイス](icorconfiguration-interface.md)
