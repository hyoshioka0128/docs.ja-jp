---
title: StrongNameGetPublicKeyEx メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName2.StrongNameGetPublicKeyEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StrongNameGetPublicKeyEx
helpviewer_keywords:
- StrongNameGetPublicKeyEx method, ICLRStrongName2 interface [.NET Framework hosting]
- ICLRStrongName2::StrongNameGetPublicKeyEx method [.NET Framework hosting]
ms.assetid: 63d8260c-fb32-4f8f-a357-768afd570f68
topic_type:
- apiref
ms.openlocfilehash: 1904a98f254a988ce035847a4cdeede182aa07bf
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84006377"
---
# <a name="strongnamegetpublickeyex-method"></a>StrongNameGetPublicKeyEx メソッド
公開キーと秘密キーのペアから公開キーを取得し、ハッシュアルゴリズムと署名アルゴリズムを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameGetPublicKey (
    [in]  LPCWSTR   pwzKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
    [in]  ULONG     uHashAlgId,  
    [in]  ULONG     uReserved,  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzKeyContainer`  
 から公開キーと秘密キーのペアを格納するキーコンテナーの名前。 `pbKeyBlob`が null の場合、では、 `szKeyContainer` 暗号化サービスプロバイダー (CSP) 内の有効なコンテナーを指定する必要があります。 この場合、メソッドは、 `StrongNameGetPublicKeyEx` コンテナーに格納されているキーペアから公開キーを抽出します。  
  
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
  
 `uHashAlgId`  
 からアセンブリハッシュアルゴリズム。 許容される値の一覧については、「解説」を参照してください。  
  
 `uReserved`  
 から将来使用するために予約されています。既定値は null です。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>コメント  
 公開キーは[Publickeyblob](../strong-naming/publickeyblob-structure.md)構造に含まれています。  
  
## <a name="remarks"></a>コメント  
 次の表は、パラメーターで許容される値のセットを示して `uHashAlgId` います。  
  
|名前|値|  
|----------|-----------|  
|なし|0|  
|SHA-1|0x8004|  
|SHA-256|0x800c|  
|SHA-384|0x800d|  
|SHA-512|0x800e|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameTokenFromPublicKey メソッド](iclrstrongname-strongnametokenfrompublickey-method.md)
- [PublicKeyBlob 構造体](../strong-naming/publickeyblob-structure.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
- [StrongNameGetPublicKey メソッド](iclrstrongname-strongnamegetpublickey-method.md)
