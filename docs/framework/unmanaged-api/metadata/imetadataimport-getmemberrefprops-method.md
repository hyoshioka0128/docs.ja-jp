---
title: IMetaDataImport::GetMemberRefProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberRefProps
helpviewer_keywords:
- GetMemberRefProps method [.NET Framework metadata]
- IMetaDataImport::GetMemberRefProps method [.NET Framework metadata]
ms.assetid: 0ea73055-ece0-4151-a094-414c88ef8941
topic_type:
- apiref
ms.openlocfilehash: 00693f1a87334620442e8865e76183b2dab68878
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503617"
---
# <a name="imetadataimportgetmemberrefprops-method"></a>IMetaDataImport::GetMemberRefProps メソッド
指定したトークンによって参照されるメンバーに関連付けられているメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMemberRefProps (  
   [in]  mdMemberRef       mr,
   [out] mdToken           *ptk,
   [out] LPWSTR            szMember,
   [in]  ULONG             cchMember,
   [out] ULONG             *pchMember,
   [out] PCCOR_SIGNATURE   *ppvSigBlob,
   [out] ULONG             *pbSig
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mr`  
 から関連付けられたメタデータを返す MemberRef トークン。  
  
 `ptk`  
 入出力メンバーを宣言するクラスを表す TypeDef または TypeRef または TypeSpec トークン、またはメンバーを宣言するモジュールクラスを表す ModuleRef トークン、またはメンバーを表す MethodDef。  
  
 `szMember`  
 入出力メンバーの名前の文字列バッファー。  
  
 `cchMember`  
 からのワイド文字で要求されたサイズ `szMember` 。  
  
 `pchMember`  
 入出力のワイド文字で返されたサイズ `szMember` 。  
  
 `ppvSibBlob`  
 入出力メンバーのバイナリメタデータシグネチャへのポインター。  
  
 `pbSig`  
 入出力のサイズ (バイト単位) `ppvSigBlob` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
