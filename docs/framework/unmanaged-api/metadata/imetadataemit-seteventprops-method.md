---
title: IMetaDataEmit::SetEventProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetEventProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetEventProps
helpviewer_keywords:
- IMetaDataEmit::SetEventProps method [.NET Framework metadata]
- SetEventProps method [.NET Framework metadata]
ms.assetid: 3b039e50-63ec-4730-99ff-2327408de477
topic_type:
- apiref
ms.openlocfilehash: 720133e64c02aa09c9ff7e43a20630b0d55c1acf
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008756"
---
# <a name="imetadataemitseteventprops-method"></a>IMetaDataEmit::SetEventProps メソッド
[IMetaDataEmit::D efineEvent](imetadataemit-defineevent-method.md)の前の呼び出しで定義されたイベントの指定された機能を設定または更新します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetEventProps (  
    [in]  mdEvent     ev,
    [in]  DWORD       dwEventFlags,
    [in]  mdToken     tkEventType,
    [in]  mdMethodDef mdAddOn,
    [in]  mdMethodDef mdRemoveOn,
    [in]  mdMethodDef mdFire,
    [in]  mdMethodDef rmdOtherMethods[]
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ev`  
 からイベントトークン。  
  
 `dwEventFlags`  
 からイベントフラグ。 これは、値のビットマスクです `CorEventAttr` 。  
  
 `tkEventType`  
 からイベントクラスのトークン。 これは、 `mdTypeDef` またはトークンのいずれか `mdTypeRef` です。  
  
 `mdAddOn`  
 からイベントの定期受信に使用するメソッド、または null。  
  
 `mdRemoveOn`  
 からイベントのサブスクリプションを解除するために使用するメソッド、または null。  
  
 `mdFire`  
 からイベントを発生させるために (派生クラスによって) 使用されるメソッド。  
  
 `rmdOtherMethods[]`  
 からイベントに関連付けられている他のメソッドのトークンの配列。 配列の最後の要素は、である必要があり `mdMethodDefNil` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
