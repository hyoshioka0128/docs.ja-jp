---
title: _CorValidateImage 関数
ms.date: 03/30/2017
api_name:
- _CorValidateImage
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- _CorValidateImage
helpviewer_keywords:
- _CorValidateImage function [.NET Framework hosting]
ms.assetid: 0117e080-05f9-4772-885d-e1847230947c
topic_type:
- apiref
ms.openlocfilehash: 426b39aa3d1ada5ae44565a742b70681a7bcf6d3
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493475"
---
# <a name="_corvalidateimage-function"></a>_CorValidateImage 関数
マネージド モジュール イメージを検証し、それらが読み込まれると、オペレーティング システム ローダーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
STDAPI _CorValidateImage (
   [in] PVOID* ImageBase,  
   [in] LPCWSTR FileName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ImageBase`  
 からマネージコードとして検証するイメージの開始位置へのポインター。 イメージは既にメモリに読み込まれている必要があります。  
  
 `FileName`  
 からイメージのファイル名。  
  
## <a name="return-value"></a>戻り値  
 この関数は、標準値、、 `E_INVALIDARG` `E_OUTOFMEMORY` 、およびを返し `E_UNEXPECTED` `E_FAIL` ます。次の値も返されます。  
  
|戻り値|説明|  
|------------------|-----------------|  
|`STATUS_INVALID_IMAGE_FORMAT`|イメージが無効です。 この値には HRESULT 0xC000007BL があります。|  
|`STATUS_SUCCESS`|イメージは有効です。 この値には、HRESULT 0x00000000L が含まれています。|  
  
## <a name="remarks"></a>解説  
 Windows XP 以降のバージョンでは、オペレーティングシステムローダーは、Common Object File Format (COFF) ヘッダーの COM 記述子ディレクトリビットを調べて、マネージモジュールをチェックします。 セットビットはマネージモジュールを示します。 ローダーがマネージモジュールを検出すると、Mscoree.dll を読み込み、を呼び出します `_CorValidateImage` 。これにより、次のアクションが実行されます。  
  
- イメージが有効なマネージモジュールであることを確認します。  
  
- イメージのエントリポイントを共通言語ランタイム (CLR) のエントリポイントに変更します。  
  
- Windows の64ビットバージョンでは、PE32 から PE32 + 形式に変換することによって、メモリ内のイメージを変更します。  
  
- マネージモジュールイメージが読み込まれると、ローダーに戻ります。  
  
 実行可能イメージの場合、オペレーティングシステムローダーは、実行可能ファイルで指定されたエントリポイントに関係なく、 [_CorExeMain](corexemain-function.md)関数を呼び出します。 DLL アセンブリイメージの場合、ローダーは[_CorDllMain](cordllmain-function.md)関数を呼び出します。  
  
 `_CorExeMain`またはは `_CorDllMain` 、次の操作を実行します。  
  
- CLR を初期化します。  
  
- アセンブリの CLR ヘッダーからマネージエントリポイントを検索します。  
  
- 実行を開始します。  
  
 ローダーは、マネージモジュールイメージがアンロードされるときに[_CorImageUnloading](corimageunloading-function.md)関数を呼び出します。 ただし、この関数は何のアクションも実行しません。これはだけを返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ グローバル静的関数](../metadata/metadata-global-static-functions.md)
