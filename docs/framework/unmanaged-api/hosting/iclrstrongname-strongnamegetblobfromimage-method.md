---
title: ICLRStrongName::StrongNameGetBlobFromImage メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameGetBlobFromImage
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameGetBlobFromImage
helpviewer_keywords:
- StrongNameGetBlobFromImage method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameGetBlobFromImage method [.NET Framework hosting]
ms.assetid: 0f5a2ec8-e776-4fd8-bda6-937b6834575a
topic_type:
- apiref
ms.openlocfilehash: 82e18db2f5b911f0e7895959119edd7d2c722f3b
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83763132"
---
# <a name="iclrstrongnamestrongnamegetblobfromimage-method"></a>ICLRStrongName::StrongNameGetBlobFromImage メソッド
指定したメモリ アドレスにあるアセンブリ イメージのバイナリ表現が取得されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameGetBlobFromImage (  
    [in]  BYTE        *pbBase,  
    [in]  DWORD       dwLength,  
    [in]  BYTE        *pbBlob,  
    [in, out] DWORD   *pcbBlob  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbBase`  
 からマップされたアセンブリマニフェストのメモリアドレス。  
  
 `dwLength`  
 からにあるイメージのサイズ (バイト単位) `pbBase` 。  
  
 `pbBlob`  
 からイメージのバイナリ表現を格納するバッファー。  
  
 `pcbBlob`  
 [入力、出力]要求された最大サイズ (バイト単位) `pbBlob` 。 戻り時に、の実際のサイズ (バイト単位) `pbBlob` 。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameGetBlob メソッド](iclrstrongname-strongnamegetblob-method.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
