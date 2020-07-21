---
title: StrongNameTokenFromPublicKey 関数
ms.date: 03/30/2017
api_name:
- StrongNameTokenFromPublicKey
api_location:
- mscoree.dll
- mscorsn.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- COM
f1_keywords:
- StrongNameTokenFromPublicKey
helpviewer_keywords:
- StrongNameTokenFromPublicKey function [.NET Framework strong naming]
ms.assetid: 997e9e57-abb2-4217-bf20-1df621a75add
topic_type:
- apiref
ms.openlocfilehash: 20be3114908ef78966eead05ae8ba6333a491404
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175058"
---
# <a name="strongnametokenfrompublickey-function"></a>StrongNameTokenFromPublicKey 関数
公開キーを表すトークンが取得されます。 厳密な名前トークンは、公開キーの短縮形です。  
  
 この関数は廃止されました。 代わりに[、メソッド](../hosting/iclrstrongname-strongnametokenfrompublickey-method.md)を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
BOOLEANStrongNameTokenFromPublicKey (
    [in]  BYTE    *pbPublicKeyBlob,  
    [in]  ULONG   cbPublicKeyBlob,  
    [out] BYTE    **ppbStrongNameToken,  
    [out] ULONG   *pcbStrongNameToken  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbPublicKeyBlob`  
 [in]厳密な名前の署名を生成するために使用されるキー ペアのパブリック部分を含む[、型の PublicKeyBlob](publickeyblob-structure.md)の構造体。  
  
 `cbPublicKeyBlob`  
 [in]のサイズ (バイト単位)`pbPublicKeyBlob`です。  
  
 `ppbStrongNameToken`  
 [アウト]渡されたキーに対応する厳密な名前トークン`pbPublicKeyBlob`。 共通言語ランタイムは、トークンを返すメモリを割り当てます。 呼び出し元は[、厳密な名前フリーバッファー](strongnamefreebuffer-function.md)関数を使用して、このメモリを解放する必要があります。  
  
 `pcbStrongNameToken`  
 [アウト]返された厳密な名前トークンのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 `true`正常に完了した場合。それ以外`false`の場合は、 .  
  
## <a name="remarks"></a>解説  
 厳密な名前トークンは、メタデータにキー情報を格納するときに領域を節約するために使用される公開キーの短縮形です。 特に、厳密な名前トークンは、依存アセンブリを参照するためにアセンブリ参照で使用されます。  
  
 関数が`StrongNameTokenFromPublicKey`正常に完了しない場合は、[関数](strongnameerrorinfo-function.md)を呼び出して、最後に生成されたエラーを取得します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** mscoree.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameTokenFromPublicKey メソッド](../hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [StrongNameGetPublicKey メソッド](../hosting/iclrstrongname-strongnamegetpublickey-method.md)
- [PublicKeyBlob 構造体](publickeyblob-structure.md)
