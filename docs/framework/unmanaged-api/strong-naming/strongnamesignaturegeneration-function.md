---
title: StrongNameSignatureGeneration 関数
ms.date: 03/30/2017
api_name:
- StrongNameSignatureGeneration
api_location:
- mscoree.dll
- mscorsn.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureGeneration
helpviewer_keywords:
- StrongNameSignatureGeneration function [.NET Framework strong naming]
ms.assetid: 839b765c-3e41-44ce-bf1b-dc10453db18e
ms.openlocfilehash: d7f481e5c61ec65d2e7414bd47227866f3435028
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176904"
---
# <a name="strongnamesignaturegeneration-function"></a>StrongNameSignatureGeneration 関数
指定したアセンブリに対して厳密な名前の署名が生成されます。  
  
 この関数は廃止されました。 代わりに[、メソッド](../hosting/iclrstrongname-strongnamesignaturegeneration-method.md)を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
BOOLEAN StrongNameSignatureGeneration (
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
 [in]厳密な名前の署名が生成されるアセンブリのマニフェストを含むファイルへのパス。  
  
 `wszKeyContainer`  
 [in]公開キーと秘密キーのペアを含むキー コンテナーの名前。  
  
 null`pbKeyBlob`の場合`wszKeyContainer`は、暗号化サービス プロバイダー (CSP) 内で有効なコンテナーを指定する必要があります。 この場合、コンテナーに格納されているキーペアを使用してファイルに署名します。  
  
 null`pbKeyBlob`でない場合、キー ペアは、キー のバイナリ ラージ オブジェクト (BLOB) に含まれていると見なされます。  
  
 キーは、1024 ビットのリベスト シャミール-アドレマン (RSA) 署名キーである必要があります。 現時点では、他の種類のキーはサポートされていません。  
  
 `pbKeyBlob`  
 [in]公開キーと秘密キーのペアへのポインター。 このペアは、Win32`CryptExportKey`関数によって作成された形式です。 null`pbKeyBlob`の場合、指定されたキー`wszKeyContainer`コンテナーにはキー ペアが含まれるものと見なされます。  
  
 `cbKeyBlob`  
 [in]のサイズ (バイト単位)`pbKeyBlob`です。  
  
 `ppbSignatureBlob`  
 [アウト]共通言語ランタイムが署名を返す場所へのポインター。 null`ppbSignatureBlob`の場合、ランタイムは、 で指定されたファイルに`wszFilePath`署名を格納します。  
  
 null`ppbSignatureBlob`でない場合、共通言語ランタイムは、署名を返す領域を割り当てます。 呼び出し元は[、厳密な名前フリーバッファー](strongnamefreebuffer-function.md)関数を使用して、この領域を解放する必要があります。  
  
 `pcbSignatureBlob`  
 [アウト]返されたシグネチャのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 `true`正常に完了した場合。それ以外`false`の場合は、 .  
  
## <a name="remarks"></a>解説  
 署名を`wszFilePath`作成せずに署名のサイズを計算するには、 に null を指定します。  
  
 署名は、ファイルに直接格納するか、または呼び出し元に返すことができます。  
  
 関数が`StrongNameSignatureGeneration`正常に完了しない場合は、[関数](strongnameerrorinfo-function.md)を呼び出して、最後に生成されたエラーを取得します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameSignatureGeneration メソッド](../hosting/iclrstrongname-strongnamesignaturegeneration-method.md)
- [StrongNameSignatureGenerationEx メソッド](../hosting/iclrstrongname-strongnamesignaturegenerationex-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
