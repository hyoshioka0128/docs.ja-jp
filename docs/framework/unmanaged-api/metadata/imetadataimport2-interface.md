---
title: IMetaDataImport2 インターフェイス
ms.date: 03/30/2017
api_name:
- IMetaDataImport2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2
helpviewer_keywords:
- IMetaDataImport2 interface [.NET Framework metadata]
ms.assetid: d39b2b87-ba53-4771-ae53-952a68452511
topic_type:
- apiref
ms.openlocfilehash: fe9e87618291218a41e52f80198ce9068c9c56e2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490396"
---
# <a name="imetadataimport2-interface"></a>IMetaDataImport2 インターフェイス
[IMetaDataImport](imetadataimport-interface.md)インターフェイスを拡張して、ジェネリック型を処理する機能を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumGenericParamConstraints メソッド](imetadataimport2-enumgenericparamconstraints-method.md)|指定したトークンによって表されるジェネリックパラメーターに関連付けられているジェネリックパラメーター制約の配列の列挙子を取得します。|  
|[EnumGenericParams メソッド](imetadataimport2-enumgenericparams-method.md)|指定した TypeDef または MethodDef トークンに関連付けられているジェネリックパラメータートークンの配列の列挙子を取得します。|  
|[EnumMethodSpecs メソッド](imetadataimport2-enummethodspecs-method.md)|指定した MethodDef または MemberRef トークンに関連付けられている MethodSpec トークンの配列の列挙子を取得します。|  
|[GetGenericParamConstraintProps メソッド](imetadataimport2-getgenericparamconstraintprops-method.md)|指定された制約トークンによって表されるジェネリックパラメーター制約に関連付けられているメタデータを取得します。|  
|[GetGenericParamProps メソッド](imetadataimport2-getgenericparamprops-method.md)|指定したトークンによって表されるジェネリックパラメーターに関連付けられているメタデータを取得します。|  
|[GetMethodSpecProps メソッド](imetadataimport2-getmethodspecprops-method.md)|指定した MethodSpec トークンによって参照されるメソッドのメタデータシグネチャを取得します。|  
|[GetPEKind メソッド](imetadataimport2-getpekind-method.md)|移植可能な実行可能 (PE) ファイルのコードの性質を示す値を取得します。通常は、現在のメタデータスコープで定義されている DLL または EXE ファイルです。|  
|[GetVersionString メソッド](imetadataimport2-getversionstring-method.md)|アセンブリのビルドに使用されたランタイムのバージョン番号を取得します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Reflection.PortableExecutableKinds>
- [メタデータ インターフェイス](metadata-interfaces.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
