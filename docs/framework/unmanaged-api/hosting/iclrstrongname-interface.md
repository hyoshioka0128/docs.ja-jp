---
title: ICLRStrongName インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRStrongName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName
helpviewer_keywords:
- ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 2fac66fd-6b3b-4dbd-8baf-86038bd85526
topic_type:
- apiref
ms.openlocfilehash: 0b6efcbe4458977e8e938afabd7ae59171bc065a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501652"
---
# <a name="iclrstrongname-interface"></a>ICLRStrongName インターフェイス
厳密な名前でアセンブリに署名するための基本的なグローバル静的関数を提供します。 すべて `ICLRStrongName` のメソッドは、標準 COM hresult を返します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetHashFromAssemblyFile メソッド](iclrstrongname-gethashfromassemblyfile-method.md)|指定したハッシュ アルゴリズムを使用して、指定したアセンブリ ファイルのハッシュ値が取得されます。|  
|[GetHashFromAssemblyFileW メソッド](iclrstrongname-gethashfromassemblyfilew-method.md)|指定したハッシュ アルゴリズムを使用して、Unicode 文字列として指定したアセンブリ ファイルのハッシュ値が取得されます。|  
|[GetHashFromBlob メソッド](iclrstrongname-gethashfromblob-method.md)|指定したハッシュ アルゴリズムを使用して、指定したメモリ アドレスにあるアセンブリのハッシュが取得されます。|  
|[GetHashFromFile メソッド](iclrstrongname-gethashfromfile-method.md)|指定したファイルの内容に対してハッシュが生成されます。|  
|[GetHashFromFileW メソッド](iclrstrongname-gethashfromfilew-method.md)|Unicode 文字列で指定されたファイルの内容に対してハッシュが作成されます。|  
|[GetHashFromHandle メソッド](iclrstrongname-gethashfromhandle-method.md)|指定したハッシュ アルゴリズムを使用して、指定したファイル ハンドルを含むファイルの内容に対してハッシュが作成されます。|  
|[StrongNameCompareAssemblies メソッド](iclrstrongname-strongnamecompareassemblies-method.md)|厳密な名前の署名に基づいて 2 つのアセンブリが異なるかどうかが判定されます。|  
|[StrongNameFreeBuffer メソッド](iclrstrongname-strongnamefreebuffer-method.md)|[StrongNameGetPublicKey](iclrstrongname-strongnamegetpublickey-method.md)、 [StrongNameTokenFromPublicKey](iclrstrongname-strongnametokenfrompublickey-method.md)、 [StrongNameSignatureGeneration](iclrstrongname-strongnamesignaturegeneration-method.md)などの厳密な名前のメソッドに対する以前の呼び出しで割り当てられたメモリを解放します。|  
|[StrongNameGetBlob メソッド](iclrstrongname-strongnamegetblob-method.md)|指定したアドレスにある実行可能ファイルのバイナリ表現が、指定したバッファーに入れられます。|  
|[StrongNameGetBlobFromImage メソッド](iclrstrongname-strongnamegetblobfromimage-method.md)|指定したメモリ アドレスにあるアセンブリ イメージのバイナリ表現が取得されます。|  
|[StrongNameGetPublicKey メソッド](iclrstrongname-strongnamegetpublickey-method.md)|秘密/公開キーの組から公開キーが取得されます。|  
|[StrongNameHashSize メソッド](iclrstrongname-strongnamehashsize-method.md)|指定したハッシュ アルゴリズムを使用して、ハッシュに必須のバッファー サイズが取得されます。|  
|[StrongNameKeyDelete メソッド](iclrstrongname-strongnamekeydelete-method.md)|指定したキー コンテナーが削除されます。|  
|[StrongNameKeyGen メソッド](iclrstrongname-strongnamekeygen-method.md)|厳密な名前を使用するために新しい公開/秘密キーの組が作成されます。|  
|[StrongNameKeyGenEx メソッド](iclrstrongname-strongnamekeygenex-method.md)|厳密な名前を使用するために、指定したキー サイズによって新しい公開/秘密キーの組が作成されます。|  
|[StrongNameKeyInstall メソッド](iclrstrongname-strongnamekeyinstall-method.md)|公開/秘密キーの組がコンテナーにインポートされます。|  
|[StrongNameSignatureGeneration メソッド](iclrstrongname-strongnamesignaturegeneration-method.md)|指定したアセンブリに対して厳密な名前の署名が生成されます。|  
|[StrongNameSignatureGenerationEx メソッド](iclrstrongname-strongnamesignaturegenerationex-method.md)|指定したフラグに基づいて、指定したアセンブリに対する厳密な名前の署名が作成されます。|  
|[StrongNameSignatureSize メソッド](iclrstrongname-strongnamesignaturesize-method.md)|厳密な名前の署名のサイズが返されます。|  
|[StrongNameSignatureVerification メソッド](iclrstrongname-strongnamesignatureverification-method.md)|指定したパスにあるアセンブリ マニフェストに厳密な名前の署名が含まれるかどうかを示す値が取得されます。これは指定したフラグに従って確認されます。|  
|[StrongNameSignatureVerificationEx メソッド](iclrstrongname-strongnamesignatureverificationex-method.md)|指定したパスにあるアセンブリ マニフェストに厳密な名前の署名が含まれるかどうかを示す値が取得されます。|  
|[StrongNameSignatureVerificationFromImage メソッド](iclrstrongname-strongnamesignatureverificationfromimage-method.md)|メモリに既にマップされているアセンブリが、関連付けられている公開キーに対して有効であるかどうかが確認されます。|  
|[StrongNameTokenFromAssembly メソッド](iclrstrongname-strongnametokenfromassembly-method.md)|指定したアセンブリ ファイルから、厳密な名前トークンが作成されます。|  
|[StrongNameTokenFromAssemblyEx メソッド](iclrstrongname-strongnametokenfromassemblyex-method.md)|指定したアセンブリ ファイルから厳密な名前のトークンが作成され、公開キーが返されます。|  
|[StrongNameTokenFromPublicKey メソッド](iclrstrongname-strongnametokenfrompublickey-method.md)|公開キーを表すトークンが取得されます。|  
  
## <a name="remarks"></a>解説  
 `ICLRStrongName`パラメーターとしておよびを使用して[ICLRRuntimeInfo:: getinterface](iclrruntimeinfo-getinterface-method.md)メソッドを呼び出すことにより、のインスタンスを取得でき `CLSID_CLRStrongName` `IID_ICLRStrongName` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
