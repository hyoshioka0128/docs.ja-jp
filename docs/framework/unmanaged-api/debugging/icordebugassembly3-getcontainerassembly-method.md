---
title: ICorDebugAssembly3::GetContainerAssembly メソッド
ms.date: 03/30/2017
ms.assetid: f5fddeb6-b82e-4ebb-b432-849ce8513c77
ms.openlocfilehash: 068a08d70f2443edfe0970ec1ffb8cba9953c6b9
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894848"
---
# <a name="icordebugassembly3getcontainerassembly-method"></a>ICorDebugAssembly3::GetContainerAssembly メソッド
この `ICorDebugAssembly3` オブジェクトのコンテナー アセンブリを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetContainerAssembly(  
    ICorDebugAssembly **ppAssembly  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppAssembly`  
 コンテナーアセンブリを表す、オブジェクトのアドレスへのポインター。メソッドの呼び出しが失敗した場合は**null** 。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドの呼び出しが成功した場合は。それ以外`S_FALSE`の場合`ppAssembly` 、、、およびは**null**になります。  
  
## <a name="remarks"></a>解説  
 このアセンブリが 1 つのコンテナー アセンブリ内の他のアセンブリとマージされている場合、このメソッドはコンテナー アセンブリを返します。 詳細と用語については、「 [ICorDebugProcess6:: EnableVirtualModuleSplitting](icordebugprocess6-enablevirtualmodulesplitting-method.md) 」を参照してください。  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugAssembly3 インターフェイス](icordebugassembly3-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
