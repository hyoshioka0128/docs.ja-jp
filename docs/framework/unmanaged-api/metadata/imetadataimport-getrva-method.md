---
title: IMetaDataImport::GetRVA メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetRVA
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetRVA
helpviewer_keywords:
- GetRVA method [.NET Framework metadata]
- IMetaDataImport::GetRVA method [.NET Framework metadata]
ms.assetid: ea422217-988b-4acd-b2db-c55357938275
topic_type:
- apiref
ms.openlocfilehash: 58ab9ee9381fce4d7af1910df6c8d3bb813bcf13
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490893"
---
# <a name="imetadataimportgetrva-method"></a>IMetaDataImport::GetRVA メソッド
指定したトークンによって表されるメソッドまたはフィールドの相対仮想アドレス (RVA) および実装フラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRVA (  
   [in]  mdToken     tk,
   [out] ULONG       *pulCodeRVA,
   [out]  DWORD      *pdwImplFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 からRVA を返すコードオブジェクトを表す MethodDef または FieldDef のメタデータトークン。 トークンが FieldDef の場合、フィールドはグローバル変数である必要があります。  
  
 `pulCodeRVA`  
 入出力トークンによって表されるコードオブジェクトの相対仮想アドレスへのポインター。  
  
 `pdwImplFlags`  
 入出力メソッドの実装フラグへのポインター。 この値は[Cormethodimpl](cormethodimpl-enumeration.md)列挙子のビットマスクです。 の値は、 `pdwImplFlags` `tk` が MethodDef トークンの場合にのみ有効です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
