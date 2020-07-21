---
title: LoadStringRC 関数
ms.date: 03/30/2017
api_name:
- LoadStringRC
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- LoadStringRC
helpviewer_keywords:
- LoadStringRC function [.NET Framework hosting]
ms.assetid: 752e49b4-987c-4c28-a118-1a0c1ed510c5
topic_type:
- apiref
ms.openlocfilehash: 8bd0292ddf22453f8892ed8bddd10c2144877097
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008517"
---
# <a name="loadstringrc-function"></a>LoadStringRC 関数
現在のスレッドの既定のカルチャを使用して、HRESULT 値をエラー メッセージに変換します。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LoadStringRC (  
    [in]  UINT    iResourceID,
    [out] LPWSTR  szBuffer,
    [in]  int     iMax,
    [in]  int     bQuiet  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `iResourceID`  
 からHRESULT。  
  
 `szBuffer`  
 入出力正常に完了したときのエラーメッセージを格納するバッファー。  
  
 `iMax`  
 からエラーメッセージバッファーのサイズ。  
  
 `bQuiet`  
 から無効.  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の値に加えて、Winerror.h で定義されている標準のコンポーネントオブジェクトモデル (COM) エラーコードを返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_INVALIDARG|`szBuffer`が null または `iMax` がゼロ (0) です。|  
  
## <a name="remarks"></a>コメント  
 メソッドが正常に完了しなかった場合、には `szBuffer` 空の文字列が含まれます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll と Mscorwks.dll。 Mscorwks.dll の代わりに Mscoree.dll を使用して、.NET Framework の正しいバージョンをターゲットにするようにしてください。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [LoadStringRCEx 関数](loadstringrcex-function.md)
- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
