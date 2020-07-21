---
title: ICLRStrongName::StrongNameSignatureGeneration メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureGeneration
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureGeneration
helpviewer_keywords:
- StrongNameSignatureGeneration method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameSignatureGeneration method [.NET Framework hosting]
ms.assetid: 4cdb1284-947a-4ed4-94c1-c5ff5cdfce56
topic_type:
- apiref
ms.openlocfilehash: a8c9eab719f6a4f233490e544f67cf779ea10b20
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83763040"
---
# <a name="iclrstrongnamestrongnamesignaturegeneration-method"></a>ICLRStrongName::StrongNameSignatureGeneration メソッド
指定したアセンブリに対して厳密な名前の署名が生成されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameSignatureGeneration (
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `wszFilePath`  
 から厳密な名前の署名が生成されるアセンブリのマニフェストを含むファイルへのパス。  
  
 `wszKeyContainer`  
 から公開キーと秘密キーのペアを格納するキーコンテナーの名前。  
  
 `pbKeyBlob`が null の場合、では、 `wszKeyContainer` 暗号化サービスプロバイダー (CSP) 内の有効なコンテナーを指定する必要があります。 この場合、コンテナーに格納されているキーペアがファイルの署名に使用されます。  
  
 `pbKeyBlob`が null でない場合、キーペアは、バイナリラージオブジェクト (BLOB) に格納されていると見なされます。  
  
 キーは 1024-Rivest-shamir-adleman-Rivest-shamir-adleman (RSA) 署名キーである必要があります。 この時点では、他の種類のキーはサポートされていません。  
  
 `pbKeyBlob`  
 から公開/秘密キーのペアへのポインター。 このペアは、Win32 関数によって作成される形式です `CryptExportKey` 。 `pbKeyBlob`が null の場合、によって指定されたキーコンテナーには、キーのペアが含まれていると `wszKeyContainer` 見なされます。  
  
 `cbKeyBlob`  
 からのサイズ (バイト単位) `pbKeyBlob` 。  
  
 `ppbSignatureBlob`  
 入出力共通言語ランタイムが署名を返す場所へのポインター。 `ppbSignatureBlob`が null の場合、ランタイムはによって指定されたファイルに署名を格納し `wszFilePath` ます。  
  
 `ppbSignatureBlob`が null でない場合は、共通言語ランタイムによって、署名を返す領域が割り当てられます。 呼び出し元は、 [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md)メソッドを使用して、この領域を解放する必要があります。  
  
 `pcbSignatureBlob`  
 入出力返されたシグネチャのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 `wszFilePath`署名を作成せずに署名のサイズを計算するには、に null を指定します。  
  
 署名は、ファイルに直接格納するか、呼び出し元に返すことができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameSignatureGenerationEx メソッド](iclrstrongname-strongnamesignaturegenerationex-method.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
