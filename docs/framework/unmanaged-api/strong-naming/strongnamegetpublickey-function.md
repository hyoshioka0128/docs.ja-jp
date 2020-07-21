---
title: StrongNameGetPublicKey 関数
ms.date: 03/30/2017
api_name:
- StrongNameGetPublicKey
api_location:
- mscoree.dll
- mscorsn.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameGetPublicKey
helpviewer_keywords:
- StrongNameGetPublicKey function [.NET Framework strong naming]
ms.assetid: 5b58c87f-3f72-40df-9b9a-291076931cc3
topic_type:
- apiref
ms.openlocfilehash: fcdd4a3f07b4499fd2388b5d165c409da9150466
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176930"
---
# <a name="strongnamegetpublickey-function"></a>StrongNameGetPublicKey 関数
秘密/公開キーの組から公開キーが取得されます。 キー ペアは、暗号化サービス プロバイダー (CSP) 内のキー コンテナー名またはバイトの生のコレクションとして提供できます。  
  
 この関数は廃止されました。 代わりに[、メソッド](../hosting/iclrstrongname-strongnamegetpublickey-method.md)を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
BOOLEAN StrongNameGetPublicKey (
    [in]  LPCWSTR   szKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szKeyContainer`  
 [in]公開キーと秘密キーのペアを含むキー コンテナーの名前。 null`pbKeyBlob`の場合`szKeyContainer`は、CSP 内で有効なコンテナーを指定する必要があります。 この場合、`StrongNameGetPublicKey`コンテナに格納されているキーペアから公開キーを抽出します。  
  
 null`pbKeyBlob`でない場合、キー ペアは、キー のバイナリ ラージ オブジェクト (BLOB) に含まれていると見なされます。  
  
 キーは、1024 ビットのリベスト シャミール-アドレマン (RSA) 署名キーである必要があります。 現時点では、他の種類のキーはサポートされていません。  
  
 `pbKeyBlob`  
 [in]公開キーと秘密キーのペアへのポインター。 このペアは、Win32`CryptExportKey`関数によって作成された形式です。 null`pbKeyBlob`の場合、指定されたキー`szKeyContainer`コンテナーにはキー ペアが含まれるものと見なされます。  
  
 `cbKeyBlob`  
 [in]のサイズ (バイト単位)`pbKeyBlob`です。  
  
 `ppbPublicKeyBlob`  
 [アウト]返された公開キー BLOB。 パラメーター`ppbPublicKeyBlob`は、共通言語ランタイムによって割り当てられ、呼び出し元に返されます。 呼び出し元は[、関数](strongnamefreebuffer-function.md)を使用してメモリを解放する必要があります。  
  
 `pcbPublicKeyBlob`  
 [アウト]返される公開キー BLOB のサイズ。  
  
## <a name="return-value"></a>戻り値  
 `true`正常に完了した場合。それ以外`false`の場合は、 .  
  
## <a name="remarks"></a>解説  
 公開キーは[、パブリックキー Blob](publickeyblob-structure.md)構造体に含まれています。  
  
 関数が`StrongNameGetPublicKey`正常に完了しない場合は、[関数](strongnameerrorinfo-function.md)を呼び出して、最後に生成されたエラーを取得します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameGetPublicKey メソッド](../hosting/iclrstrongname-strongnamegetpublickey-method.md)
- [StrongNameTokenFromPublicKey メソッド](../hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
- [PublicKeyBlob 構造体](publickeyblob-structure.md)
