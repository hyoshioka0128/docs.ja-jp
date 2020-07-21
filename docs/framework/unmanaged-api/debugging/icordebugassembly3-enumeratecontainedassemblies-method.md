---
title: ICorDebugAssembly3::EnumerateContainedAssemblies メソッド
ms.date: 03/30/2017
ms.assetid: 98f15b05-afad-4616-9e2a-1a9af31948b6
ms.openlocfilehash: aebf499d7d25caef80782cc5661a57048dc5f6a9
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894862"
---
# <a name="icordebugassembly3enumeratecontainedassemblies-method"></a>ICorDebugAssembly3::EnumerateContainedAssemblies メソッド
このアセンブリに含まれているアセンブリの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateContainedAssemblies(  
    ICorDebugAssemblyEnum **ppAssemblies  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppAssemblies`  
 [出力] 列挙子である ICorDebugAssemblyEnum インターフェイス オブジェクトのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 この `S_OK` オブジェクトがコンテナーの場合は、`ICorDebugAssembly3`。それ以外の場合は、`S_FALSE` で、列挙子は空です。  
  
## <a name="remarks"></a>解説  
 含まれているアセンブリを列挙するためにシンボルが必要です。 シンボルがない場合、メソッドは `S_FALSE` を返し、有効な列挙子は提供されません。  
  
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
