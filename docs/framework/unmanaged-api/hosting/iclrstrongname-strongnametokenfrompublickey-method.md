---
title: ICLRStrongName::StrongNameTokenFromPublicKey メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameTokenFromPublicKey
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameTokenFromPublicKey
helpviewer_keywords:
- ICLRStrongName::StrongNameTokenFromPublicKey method [.NET Framework hosting]
- StrongNameTokenFromPublicKey method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 7962ce88-7e86-4a6f-8298-621b01ffc3c2
topic_type:
- apiref
ms.openlocfilehash: e61a652072b424d1245518c832f9b0856e0f2021
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762605"
---
# <a name="iclrstrongnamestrongnametokenfrompublickey-method"></a>ICLRStrongName::StrongNameTokenFromPublicKey メソッド
公開キーを表すトークンを取得します。 厳密な名前トークンは、公開キーの短縮形です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameTokenFromPublicKey (
    [in]  BYTE    *pbPublicKeyBlob,  
    [in]  ULONG   cbPublicKeyBlob,  
    [out] BYTE    **ppbStrongNameToken,  
    [out] ULONG   *pcbStrongNameToken  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbPublicKeyBlob`  
 から厳密な名前の署名を生成するために使用されるキーペアの公開部分を格納する[Publickeyblob](../strong-naming/publickeyblob-structure.md)型の構造体。  
  
 `cbPublicKeyBlob`  
 からのサイズ (バイト単位) `pbPublicKeyBlob` 。  
  
 `ppbStrongNameToken`  
 入出力渡されたキーに対応する厳密な名前トークン `pbPublicKeyBlob` 。 共通言語ランタイムは、トークンを返すメモリを割り当てます。 呼び出し元は、 [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md)メソッドを使用して、このメモリを解放する必要があります。  
  
 `pcbStrongNameToken`  
 入出力返された厳密な名前トークンのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 厳密な名前トークンは、キー情報をメタデータに格納するときに領域を節約するために使用される公開キーの短縮形です。 具体的には、アセンブリ参照では、依存アセンブリを参照するために厳密な名前トークンが使用されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameGetPublicKey メソッド](iclrstrongname-strongnamegetpublickey-method.md)
- [PublicKeyBlob 構造体](../strong-naming/publickeyblob-structure.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
