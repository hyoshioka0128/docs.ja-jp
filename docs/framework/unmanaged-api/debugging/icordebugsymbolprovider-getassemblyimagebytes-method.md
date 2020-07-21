---
title: ICorDebugSymbolProvider::GetAssemblyImageBytes メソッド
ms.date: 03/30/2017
ms.assetid: 3db215aa-e180-4f70-8d23-6d5a0ffbc8e5
ms.openlocfilehash: a555acb9e23098b0a0f70924032771b1ae18e88e
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83376113"
---
# <a name="icordebugsymbolprovidergetassemblyimagebytes-method"></a>ICorDebugSymbolProvider::GetAssemblyImageBytes メソッド
マージされたアセンブリ内の指定の相対仮想アドレス (RVA: relative virtual address) で、マージされたアセンブリのデータを読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAssemblyImageBytes(  
   [in] CORDB_ADDRESS rva,
   [in] ULONG32 length,
   [out] ICorDebugMemoryBuffer** ppMemoryBuffer  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `rva`  
 [in] マージされたアセンブリ内の相対仮想アドレス (RVA)。  
  
 `length`  
 マージされたアセンブリから読み取るバイト数。  
  
 `ppMemoryBuffer`  
 マージされたアセンブリメタデータを持つメモリバッファーに関する情報を格納している、[のオブジェクトの](icordebugmemorybuffer-interface.md)アドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugSymbolProvider インターフェイス](icordebugsymbolprovider-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
