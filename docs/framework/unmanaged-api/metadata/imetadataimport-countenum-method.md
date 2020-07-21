---
title: IMetaDataImport::CountEnum メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.CountEnum
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::CountEnum
helpviewer_keywords:
- CountEnum method [.NET Framework metadata]
- IMetaDataImport::CountEnum method [.NET Framework metadata]
ms.assetid: d1de53ad-9435-4b5f-9df7-07f21210e5b5
topic_type:
- apiref
ms.openlocfilehash: 4521a3f15ec358a4d786a4533efb6b99d0e1c1cc
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84492383"
---
# <a name="imetadataimportcountenum-method"></a>IMetaDataImport::CountEnum メソッド
指定した列挙子によって取得された列挙体の要素の数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CountEnum (  
   [in]  HCORENUM    hEnum,
   [out] ULONG       *pulCount  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hEnum`  
 から列挙子のハンドルです。  
  
 `pulCount`  
 入出力列挙された要素の数。  
  
## <a name="remarks"></a>解説  
 によって指定されたハンドル `hEnum` は、前 `Enum` の*名前*の呼び出し (たとえば、 [IMetaDataImport:: enumtypedefs](imetadataimport-enumtypedefs-method.md)) から取得されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
