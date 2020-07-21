---
title: IMetaDataEmit::DefineEvent メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineEvent
helpviewer_keywords:
- IMetaDataEmit::DefineEvent method [.NET Framework metadata]
- DefineEvent method [.NET Framework metadata]
ms.assetid: cf064bac-9a9f-41c5-9e1d-108ff7af3afe
topic_type:
- apiref
ms.openlocfilehash: 7babd0a90b9882acb03b6360753f55c57a399b9e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84005636"
---
# <a name="imetadataemitdefineevent-method"></a>IMetaDataEmit::DefineEvent メソッド
指定したメタデータシグネチャを持つイベントの定義を作成し、そのイベント定義へのトークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineEvent (
    [in]  mdTypeDef    td,
    [in]  LPCWSTR      szEvent,
    [in]  DWORD        dwEventFlags,
    [in]  mdToken      tkEventType,
    [in]  mdMethodDef  mdAddOn,
    [in]  mdMethodDef  mdRemoveOn,
    [in]  mdMethodDef  mdFire,
    [in]  mdMethodDef  rmdOtherMethods[],
    [out] mdEvent      *pmdEvent
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 からターゲットクラスまたはインターフェイスのトークン。 これは、 `mdTypeDef` またはトークンのいずれか `mdTypeDefNil` です。  
  
 `szEvent`  
 からイベントの名前。  
  
 `dwEventFlags`  
 からイベントフラグ。  
  
 `tkEventType`  
 からイベントクラスのトークン。 これは `mdTypeDef` 、、、 `mdTypeRef` または `mdTokenNil` トークンです。  
  
 `mdAddOn`  
 からイベントの定期受信に使用するメソッド、または null。  
  
 `mdRemoveOn`  
 からイベントのサブスクリプションを解除するために使用するメソッド、または null。  
  
 `mdFire`  
 からイベントを発生させるために (派生クラスによって) 使用されるメソッド。  
  
 `rmdOtherMethods[]`  
 からイベントに関連付けられている他のメソッドのトークンの配列。 配列がトークンで終了してい `mdMethodDefNil` ます。  
  
 `pmdEvent`  
 入出力イベントに割り当てられたメタデータトークン。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
