---
title: IMetaDataImport::CloseEnum メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.CloseEnum
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::CloseEnum
helpviewer_keywords:
- IMetaDataImport::CloseEnum method [.NET Framework metadata]
- CloseEnum method, IMetaDataImport interface [.NET Framework metadata]
ms.assetid: 727819d5-1dab-4ebb-ac25-950b4111dc72
topic_type:
- apiref
ms.openlocfilehash: 5de62db4180a6a9160193053fe42e39cebc34d0e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84492494"
---
# <a name="imetadataimportcloseenum-method"></a>IMetaDataImport::CloseEnum メソッド
指定したハンドルによって識別される列挙子を閉じます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void CloseEnum (  
   [in] HCORENUM hEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hEnum`  
 から閉じる列挙子のハンドル。  
  
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
