---
title: IMetaDataImport::GetMemberProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberProps
helpviewer_keywords:
- IMetaDataImport::GetMemberProps method [.NET Framework metadata]
- GetMemberProps method [.NET Framework metadata]
ms.assetid: 42790918-4142-4938-b8f4-a56979a55846
topic_type:
- apiref
ms.openlocfilehash: 0357444aa8fa38bce5a7175cf6aacfe1a2b2b16e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503641"
---
# <a name="imetadataimportgetmemberprops-method"></a>IMetaDataImport::GetMemberProps メソッド
指定された <xref:System.Type> メタデータトークンによって参照されるメンバーの、名前、バイナリ署名、相対仮想アドレスなど、指定されたメンバー定義のメタデータに格納されている情報を取得します。 これは単純なヘルパーメソッドです。 *mb*が MethodDef の場合は、 **getmethodprops**が呼び出されます。*mb*が FieldDef の場合は、 **getfieldprops**が呼び出されます。 詳細については、これらの他の方法を参照してください。
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMemberProps (  
   [in]  mdToken           mb,
   [out] mdTypeDef         *pClass,  
   [out] LPWSTR            szMember,
   [in]  ULONG             cchMember,
   [out] ULONG             *pchMember,
   [out] DWORD             *pdwAttr,  
   [out] PCCOR_SIGNATURE   *ppvSigBlob,
   [out] ULONG             *pcbSigBlob,
   [out] ULONG             *pulCodeRVA,
   [out] DWORD             *pdwImplFlags,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppValue,  
   [out] ULONG             *pcchValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mb`  
 から関連付けられているメタデータを取得するメンバーを参照するトークン。  
  
 `pClass`  
 入出力メンバーのクラスを表すメタデータトークンへのポインター。  
  
 `szMember`  
 入出力メンバーの名前。  
  
 `cchMember`  
 からバッファーのサイズ (ワイド文字単位) `szMember` 。  
  
 `pchMember`  
 入出力返される名前のワイド文字単位のサイズ。  
  
 `pdwAttr`  
 入出力メンバーに適用されるフラグ値。  
  
 `ppvSigBlob`  
 入出力メンバーのバイナリメタデータシグネチャへのポインター。  
  
 `pcbSigBlob`  
 入出力のサイズ (バイト単位) `ppvSigBlob` 。  
  
 `pulCodeRVA`  
 入出力メンバーの相対仮想アドレスへのポインター。  
  
 `pdwImplFlags`  
 入出力メンバーに関連付けられているメソッド実装フラグ。  
  
 `pdwCPlusTypeFlag`  
 入出力をマークするフラグ <xref:System.ValueType> 。 値の1つです `ELEMENT_TYPE_*` 。
  
 `ppValue`  
 入出力このメンバーによって返される定数文字列値。  
  
 `pcchValue`  
 入出力の文字数のサイズ `ppValue` `ppValue` 。が文字列を保持しない場合は0。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
