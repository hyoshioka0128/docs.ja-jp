---
title: IMetaDataImport::GetCustomAttributeByName メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetCustomAttributeByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetCustomAttributeByName
helpviewer_keywords:
- IMetaDataImport::GetCustomAttributeByName method [.NET Framework metadata]
- GetCustomAttributeByName method [.NET Framework metadata]
ms.assetid: 909aa530-2e3b-4d0a-a38a-a2750e535d7d
topic_type:
- apiref
ms.openlocfilehash: e6921a0f6420546ba1e866e37a7a7cb129a77c67
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491460"
---
# <a name="imetadataimportgetcustomattributebyname-method"></a>IMetaDataImport::GetCustomAttributeByName メソッド
名前と所有者を指定して、カスタム属性を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCustomAttributeByName (  
   [in]  mdToken          tkObj,  
   [in]  LPCWSTR          szName,  
   [out] const void       **ppData,  
   [out] ULONG            *pcbData  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tkObj`  
 からカスタム属性を所有するオブジェクトを表すメタデータトークン。  
  
 `szName`  
 からカスタム属性の名前。  
  
 `ppData`  
 入出力カスタム属性の値であるデータの配列へのポインター。  
  
 `pcbData`  
 入出力* で返されるデータのサイズ (バイト単位) `ppData` 。  
  
## <a name="remarks"></a>解説  
 同じ所有者に対して複数のカスタム属性を定義することは有効です。同じ名前を持つ場合もあります。 ただし、は `GetCustomAttributeByName` 1 つのインスタンスのみを返します。 ( `GetCustomAttributeByName` 最初に見つかったインスタンスを返します)。カスタム属性のすべてのインスタンスを検索するには、 [IMetaDataImport:: EnumCustomAttributes](imetadataimport-enumcustomattributes-method.md)メソッドを呼び出します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
