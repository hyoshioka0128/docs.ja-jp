---
title: IMetaDataAssemblyImport::FindExportedTypeByName メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.FindExportedTypeByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::FindExportedTypeByName
helpviewer_keywords:
- FindExportedTypeByName method [.NET Framework metadata]
- IMetaDataAssemblyImport::FindExportedTypeByName method [.NET Framework metadata]
ms.assetid: 46264b2c-574d-4dde-aafc-77187a104fdd
topic_type:
- apiref
ms.openlocfilehash: ac6de9a16fad6ba9d14f3960ddd28c42c111f254
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009393"
---
# <a name="imetadataassemblyimportfindexportedtypebyname-method"></a>IMetaDataAssemblyImport::FindExportedTypeByName メソッド
名前と外側の型を指定して、エクスポートされた型へのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindExportedTypeByName (  
    [in]  LPCWSTR           szName,
    [in]  mdToken           mdtExportedType,
    [out] mdExportedType    *ptkExportedType  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szName`  
 からエクスポートされた型の名前。  
  
 `mdtExportedType`  
 からエクスポートする型の外側のクラスのメタデータトークン。 要求されたエクスポート型が入れ子にされた型では `mdExportedTypeNil` ない場合、この値はです。  
  
 `ptkExportedType`  
 入出力エクスポートされた `mdExportedType` 型を表すトークンへのポインター。  
  
## <a name="remarks"></a>コメント  
 メソッドは、 `FindExportedTypeByName` 参照を解決するために共通言語ランタイムによって採用されている標準の規則を使用します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
- [ランタイムがアセンブリを検索する方法](../../deployment/how-the-runtime-locates-assemblies.md)
