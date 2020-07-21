---
title: IMetaDataImport::GetParamProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetParamProps
helpviewer_keywords:
- IMetaDataImport::GetParamProps method [.NET Framework metadata]
- GetParamProps method [.NET Framework metadata]
ms.assetid: 4d5e5f00-bcab-4f41-b191-176511a186a7
topic_type:
- apiref
ms.openlocfilehash: c2abf2813c6e1a9db4264bded32d9cb9c58a2bcb
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491057"
---
# <a name="imetadataimportgetparamprops-method"></a>IMetaDataImport::GetParamProps メソッド
指定した ParamDef トークンによって参照されるパラメーターのメタデータ値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetParamProps (  
   [in]  mdParamDef      tk,  
   [out] mdMethodDef     *pmd,  
   [out] ULONG           *pulSequence,  
   [out] LPWSTR          szName,  
   [in]  ULONG           cchName,  
   [out] ULONG           *pchName,  
   [out] DWORD           *pdwAttr,  
   [out] DWORD           *pdwCPlusTypeFlag,  
   [out] UVCP_CONSTANT   *ppValue,  
   [out] ULONG           *pcchValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 からメタデータを返すパラメーターを表す ParamDef トークン。  
  
 `pmd`  
 入出力パラメーターを受け取るメソッドを表す MethodDef トークンへのポインター。  
  
 `pulSequence`  
 入出力メソッド引数リスト内のパラメーターの序数位置。  
  
 `szName`  
 入出力パラメーターの名前を保持するバッファー。  
  
 `cchName`  
 からのワイド文字で要求されたサイズ `szName` 。  
  
 `pchName`  
 入出力のワイド文字で返されたサイズ `szName` 。  
  
 `pdwAttr`  
 入出力パラメーターに関連付けられているすべての属性フラグへのポインター。 これは、値のビットマスクです `CorParamAttr` 。  
  
 `pdwCPlusTypeFlag`  
 入出力パラメーターがであることを示すフラグへのポインター <xref:System.ValueType> 。  
  
 `ppValue`  
 入出力パラメーターによって返される定数文字列へのポインター。  
  
 `pcchValue`  
 入出力のサイズ `ppValue` 。ワイド文字の場合は `ppValue` 。が文字列を保持しない場合は0。  
  
## <a name="remarks"></a>解説

パラメーターの場合、のシーケンス値は `pulSequence` 1 から始まります。 戻り値のシーケンス番号は0です。

## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
