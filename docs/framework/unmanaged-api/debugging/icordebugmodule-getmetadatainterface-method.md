---
title: ICorDebugModule::GetMetaDataInterface メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetMetaDataInterface
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetMetaDataInterface
helpviewer_keywords:
- ICorDebugModule::GetMetaDatainterface method [.NET Framework debugging]
- GetMetaDatainterface method [.NET Framework debugging]
ms.assetid: 30d906f2-cf35-4fa9-9d4c-0c31b58c9f3a
topic_type:
- apiref
ms.openlocfilehash: f5d0dd7a99087b21a5f827e4dce0f6342ae7b25a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501769"
---
# <a name="icordebugmodulegetmetadatainterface-method"></a>ICorDebugModule::GetMetaDataInterface メソッド
モジュールのメタデータを調べるために使用できるメタデータインターフェイスオブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMetaDataInterface (  
    [in] REFIID      riid,  
    [out] IUnknown **ppObj  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `riid`  
 からメタデータインターフェイスを指定する参照 ID。  
  
 `ppObj`  
 入出力`T:IUnknown`[メタデータインターフェイス](../metadata/metadata-interfaces.md)の1つであるオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 デバッガーは、メソッドを使用して `GetMetaDataInterface` モジュールの元のメタデータのコピーを作成できます。モジュールは、モジュールを編集するために実行する必要があります。 デバッガーはを呼び出して、 `GetMetaDataInterface` モジュールの[IMetaDataEmit](../metadata/imetadataemit-interface.md) interface オブジェクトを取得し、 [IMetaDataEmit:: savetomemory](../metadata/imetadataemit-savetomemory-method.md)を呼び出してモジュールのメタデータのコピーをメモリに保存します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [Metadata](../metadata/index.md)
