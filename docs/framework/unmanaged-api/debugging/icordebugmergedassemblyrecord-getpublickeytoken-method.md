---
title: ICorDebugMergedAssemblyRecord::GetPublicKeyToken メソッド
ms.date: 03/30/2017
ms.assetid: 72020b72-9611-4bc3-b1e7-5a16b023bfa3
ms.openlocfilehash: 4cd0ff788401a7b5d70e215209194c0eb6cad1f8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212114"
---
# <a name="icordebugmergedassemblyrecordgetpublickeytoken-method"></a>ICorDebugMergedAssemblyRecord::GetPublicKeyToken メソッド
アセンブリの公開キー トークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPublicKeyToken(  
   [in] ULONG32 cbPublicKeyToken,
   [out] ULONG32 *pcbPublicKeyToken,
   [out, size_is(cbPublicKeyToken), length_is(*pcbPublicKeyToken)] BYTE pbPublicKeyToken[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cbPublicKeyToken`  
 [in] `pbPublicKeyToken` 配列の最大バイト数。  
  
 `pcbPublicKeyToken`  
 [out] `pbPublicKeyToken` 配列への実際の書き込みバイト数へのポインター。  
  
 `pbPublicKeyToken`  
 [out] アセンブリの公開キー トークンを含むバイト配列へのポインター。  
  
## <a name="remarks"></a>Remarks  
 アセンブリの公開キー トークンは、その公開キーの SHA1 ハッシュの最後の 8 バイトです。  
  
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
