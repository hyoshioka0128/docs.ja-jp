---
title: ExportNestedType メソッド
ms.date: 03/30/2017
api_name:
- IALink.ExportNestedType
- ExportNestedType
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ExportNestedType
helpviewer_keywords:
- ExportNestedType method
ms.assetid: dec7df60-4d30-47c8-99db-72e0419e5f76
topic_type:
- apiref
ms.openlocfilehash: 9ca2167e66ac3aa5bcc0e92ff357eed18d366c67
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179415"
---
# <a name="exportnestedtype-method"></a>ExportNestedType メソッド
入れ子にされた型をエクスポート可能として指定します。 [エクスポートタイプ メソッド](exporttype-method.md)は、入れ子になった型をエクスポートすることもできますが、このメソッドの方が高速です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExportNestedType(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    mdTypeDef       TypeToken,  
    mdExportedType  ParentType,  
    LPCWSTR         pszTypename,  
    DWORD           dwFlags,  
    mdExportedType* pType  
) PURE;
```  
  
## <a name="parameters"></a>パラメーター  
 `AssemblyID`  
 エクスポートするアセンブリの ID。  
  
 `FileToken`  
 エクスポート可能にする型を定義するファイル トークンまたはファイルのアセンブリ。  
  
 `TypeToken`  
 エクスポート可能にする型のトークンを入力します。  
  
 `ParentType`  
 親タイプのトークン。  
  
 `pszTypename`  
 エクスポートする完全修飾型名。  
  
 `dwFlags`  
 `ComType`や`tdNested`などの`tdPublic`フラグ。 この値は、[エクスポートされた型のメソッド](../metadata/imetadataassemblyemit-defineexportedtype-method.md)に渡すことができます。  
  
 `pType`  
 エクスポートされた型のトークンを受け取ります。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は、S_OKを返します。  
  
## <a name="requirements"></a>必要条件  
 alink.h が必要です。  
  
## <a name="see-also"></a>関連項目

- [IALink インターフェイス](ialink-interface.md)
- [IALink2 インターフェイス](ialink2-interface.md)
- [ALink API](index.md)
