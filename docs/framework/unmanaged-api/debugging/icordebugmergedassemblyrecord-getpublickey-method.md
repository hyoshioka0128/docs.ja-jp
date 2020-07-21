---
title: ICorDebugMergedAssemblyRecord::GetPublicKey メソッド
ms.date: 03/30/2017
ms.assetid: 6f4e78ba-082b-489d-8b58-4c35fbcc7a5b
ms.openlocfilehash: 51724aa1ee6101c50c7cdb4b6071fb458814f483
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213544"
---
# <a name="icordebugmergedassemblyrecordgetpublickey-method"></a>ICorDebugMergedAssemblyRecord::GetPublicKey メソッド
アセンブリの公開キーを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPublicKey(  
   [in] ULONG32 cbPublicKey,
   [out] ULONG32 *pcbPublicKey,
   [out, size_is(cbPublicKey), length_is(*pcbPublicKey)] BYTE pbPublicKey[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cbPublicKey`  
 [in] `pbPublicKey` 配列の最大バイト数。  
  
 `pcbPublicKey`  
 [out] `pbPublicKey` 配列への実際の書き込みバイト数へのポインター。  
  
 `pbPublicKey`  
 [out] アセンブリの公開キーを含むバイト配列へのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugMergedAssemblyRecord インターフェイス](icordebugmergedassemblyrecord-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
