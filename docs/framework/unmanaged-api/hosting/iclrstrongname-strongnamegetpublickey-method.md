---
title: ICLRStrongName::StrongNameGetPublicKey メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameGetPublicKey
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameGetPublicKey
helpviewer_keywords:
- StrongNameGetPublicKey method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameGetPublicKey method [.NET Framework hosting]
ms.assetid: a31dcaa9-a404-4c1d-8cc7-081827c52935
topic_type:
- apiref
ms.openlocfilehash: 5a20bde64830617090c92afe5fae3a603cf9103b
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83763133"
---
# <a name="iclrstrongnamestrongnamegetpublickey-method"></a>ICLRStrongName::StrongNameGetPublicKey メソッド
公開キーと秘密キーのペアから公開キーを取得します。 キーペアは、暗号化サービスプロバイダー (CSP) 内のキーコンテナー名として、またはバイトの未加工コレクションとして指定できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameGetPublicKey (
    [in]  LPCWSTR   szKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szKeyContainer`  
 から公開キーと秘密キーのペアを格納するキーコンテナーの名前。 `pbKeyBlob`が null の場合、は `szKeyContainer` CSP 内の有効なコンテナーを指定する必要があります。 この場合、 [ICLRStrongName:: StrongNameGetPublicKey](iclrstrongname-strongnamegetpublickey-method.md)メソッドは、コンテナーに格納されているキーペアから公開キーを抽出します。  
  
 `pbKeyBlob`が null でない場合、キーペアは、バイナリラージオブジェクト (BLOB) に格納されていると見なされます。  
  
 キーは 1024-Rivest-shamir-adleman-Rivest-shamir-adleman (RSA) 署名キーである必要があります。 この時点では、他の種類のキーはサポートされていません。  
  
 `pbKeyBlob`  
 から公開/秘密キーのペアへのポインター。 このペアは、Win32 関数によって作成される形式です `CryptExportKey` 。 `pbKeyBlob`が null の場合、によって指定されたキーコンテナーには、キーのペアが含まれていると `szKeyContainer` 見なされます。  
  
 `cbKeyBlob`  
 からのサイズ (バイト単位) `pbKeyBlob` 。  
  
 `ppbPublicKeyBlob`  
 入出力返された公開キー BLOB。 パラメーターは、 `ppbPublicKeyBlob` 共通言語ランタイムによって割り当てられ、呼び出し元に返されます。 呼び出し元は、 [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md)メソッドを使用して、メモリを解放する必要があります。  
  
 `pcbPublicKeyBlob`  
 入出力返される公開キー BLOB のサイズ。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 公開キーは[Publickeyblob](../strong-naming/publickeyblob-structure.md)構造に含まれています。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameTokenFromPublicKey メソッド](iclrstrongname-strongnametokenfrompublickey-method.md)
- [PublicKeyBlob 構造体](../strong-naming/publickeyblob-structure.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
