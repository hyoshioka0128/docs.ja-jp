---
title: ICLRStrongName::StrongNameKeyGenEx メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameKeyGenEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameKeyGenEx
helpviewer_keywords:
- ICLRStrongName::StrongNameKeyGenEx method [.NET Framework hosting]
- StrongNameKeyGenEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 1f8b59d0-5b72-45b8-ab74-c2b43ffc806e
topic_type:
- apiref
ms.openlocfilehash: fb18b7b5ac73a1f270af6fae95a23e04b17ca5f1
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83763073"
---
# <a name="iclrstrongnamestrongnamekeygenex-method"></a>ICLRStrongName::StrongNameKeyGenEx メソッド
厳密な名前の使用のために、指定されたキーサイズを持つ新しい公開/秘密キーのペアを生成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameKeyGenEx (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  DWORD     dwFlags,  
    [in]  DWORD     dwKeySize,  
    [out] BYTE      **ppbKeyBlob,  
    [out] ULONG     *pcbKeyBlob  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `wszKeyContainer`  
 から要求されたキーコンテナー名。 `wszKeyContainer`は、空でない文字列であるか、または一時名を生成するために null である必要があります。  
  
 `dwFlags`  
 からキーを登録したままにするかどうかを示す値です。 次の値がサポートされています。  
  
- 0x00000000- `wszKeyContainer` が null の場合に、一時キーコンテナー名を生成するために使用されます。  
  
- 0x00000001 ( `SN_LEAVE_KEY` )-キーを登録したままにすることを指定します。  
  
 `dwKeySize`  
 から要求されたキーのサイズ (ビット単位)。  
  
 `ppbKeyBlob`  
 入出力返された公開/秘密キーのペア。  
  
 `pcbKeyBlob`  
 入出力のサイズ (バイト単位) `ppbKeyBlob` 。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 .NET Framework バージョン1.0 および1.1 では、 `dwKeySize` 厳密な名前でアセンブリに署名するには1024ビットが必要です。バージョン2.0 では、2048ビットキーのサポートが追加されます。  
  
 キーを取得した後、 [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md)メソッドを呼び出して、割り当てられたメモリを解放する必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameKeyGen メソッド](iclrstrongname-strongnamekeygen-method.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
