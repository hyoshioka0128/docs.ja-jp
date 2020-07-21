---
title: GetCORVersion 関数
ms.date: 03/30/2017
api_name:
- GetCORVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetCORVersion
helpviewer_keywords:
- GetCORVersion function [.NET Framework hosting]
ms.assetid: 2f09cd37-bf3a-4cc5-87b0-adc42a7eed31
topic_type:
- apiref
ms.openlocfilehash: 23d68e8e4bbd87779e3b49f0c40f5a5ab9f5124f
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83617218"
---
# <a name="getcorversion-function"></a>GetCORVersion 関数
現在のプロセスで実行されている共通言語ランタイム (CLR) のバージョン番号を返します。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCORVersion (  
    [in] LPWSTR  pbuffer,  
    [in]  DWORD   cchBuffer,
    [out] DWORD*  dwlength  
);
```  
  
## <a name="parameters"></a>パラメーター  
 `pbuffer`  
 現在プロセスに読み込まれているランタイムのバージョンを指定する文字列を CLR が返すバッファーへのポインター。 返される文字列は、 [Corbindtoruntimeex](corbindtoruntimeex-function.md)に渡される文字列と同じ形式になります (例、"v 1.0.1216")。 ランタイムがまだプロセスに読み込まれていない場合、関数はコンピューターにインストールされている最新バージョンのランタイムの適切なディレクトリ情報を返します。  
  
 `cchBuffer`  
 `WCHAR`で保持できる文字の数 `pbuffer` です。  
  
 `dwLength`  
 で実際に返された文字数へのポインター `pbuffer` 。 `pbuffer`が null ポインターの場合、ランタイムは E_POINTER を返します。 文字数がの長さを超える場合 `pbuffer` 、ランタイムは ERROR_INSUFFICIENT_BUFFER を返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
