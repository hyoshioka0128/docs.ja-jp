---
title: IMetaDataDispenserEx::GetOption メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.GetOption
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::GetOption
helpviewer_keywords:
- GetOption method [.NET Framework metadata]
- IMetaDataDispenserEx::GetOption method [.NET Framework metadata]
ms.assetid: d7f794e5-8e25-4d65-850a-7c34fbfce87d
topic_type:
- apiref
ms.openlocfilehash: 832adacac4a6df9ccf21578538a1c557150f3ba1
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008782"
---
# <a name="imetadatadispenserexgetoption-method"></a>IMetaDataDispenserEx::GetOption メソッド
現在のメタデータスコープの指定したオプションの値を取得します。 オプションは、現在のメタデータスコープへの呼び出しの処理方法を制御します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetOption (  
    [in]  REFGUID         optionId,
    [out] const VARIANT   *pValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `optionId`  
 から取得するオプションを指定する GUID へのポインター。 サポートされている Guid の一覧については、「解説」を参照してください。  
  
 `pValue`  
 入出力返されたオプションの値。 この値の型は、指定されたオプションの型のバリアントになります。  
  
## <a name="remarks"></a>コメント  
 次の一覧は、このメソッドでサポートされている Guid を示しています。 説明については、 [IMetaDataDispenserEx:: SetOption](imetadatadispenserex-setoption-method.md)メソッドを参照してください。 `optionId`がこのリストに含まれていない場合、このメソッドは HRESULT を返し `E_INVALIDARG` ます。パラメーターが正しくないことを示します。  
  
- MetaDataCheckDuplicatesFor  
  
- MetaDataRefToDefCheck  
  
- MetaDataNotificationForTokenMovement  
  
- MetaDataSetENC  
  
- MetaDataErrorIfEmitOutOfOrder  
  
- MetaDataGenerateTCEAdapters  
  
- MetaDataLinkerOptions  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataDispenserEx インターフェイス](imetadatadispenserex-interface.md)
- [IMetaDataDispenser インターフェイス](imetadatadispenser-interface.md)
