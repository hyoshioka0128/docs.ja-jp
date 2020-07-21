---
title: ICorDebugStaticFieldSymbol::GetAddress メソッド
ms.date: 03/30/2017
ms.assetid: 5a6c9a5a-ec72-4c40-a9c3-cee7baa63687
ms.openlocfilehash: 7b8072234df172eeafd77db90287ea3319c08ec7
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378768"
---
# <a name="icordebugstaticfieldsymbolgetaddress-method"></a>ICorDebugStaticFieldSymbol::GetAddress メソッド
静的フィールドのアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAddress(  
   [out] CORDB_ADDRESS *pRVA  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 pRVA  
 [out] 静的フィールドの相対仮想アドレス (RVA) へのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugStaticFieldSymbol インターフェイス](icordebugstaticfieldsymbol-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
