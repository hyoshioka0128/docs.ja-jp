---
title: ICorDebugMergedAssemblyRecord::GetVersion メソッド
ms.date: 03/30/2017
ms.assetid: c6858b06-ae26-4312-b325-ea6025016675
ms.openlocfilehash: cad71080c86e92beb318722db86011b09ce02e91
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207624"
---
# <a name="icordebugmergedassemblyrecordgetversion-method"></a>ICorDebugMergedAssemblyRecord::GetVersion メソッド
アセンブリのバージョン情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetVersion(  
   [out] USHORT *pMajor,
   [out] USHORT *pMinor,
   [out] USHORT *pBuild,
   [out] USHORT *pRevision  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pMajor`  
 [out] メジャー バージョン番号へのポインター。  
  
 `pMinor`  
 [out] マイナー バージョン番号へのポインター。  
  
 `pBuild`  
 [out] ビルド番号へのポインター。  
  
 `pRevision`  
 [out] リビジョン番号へのポインター。  
  
## <a name="remarks"></a>Remarks  
 アセンブリのバージョン番号については、<xref:System.Version> クラスのトピックを参照してください。  
  
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
