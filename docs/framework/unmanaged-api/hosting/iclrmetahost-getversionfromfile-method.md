---
title: ICLRMetaHost::GetVersionFromFile メソッド
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.GetVersionFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::GetVersionFromFile
helpviewer_keywords:
- ICLRMetaHost::GetVersionFromFile method [.NET Framework hosting]
- GetVersionFromFile method [.NET Framework hosting]
ms.assetid: 55bb3eb4-f665-42fc-973c-465567570e82
topic_type:
- apiref
ms.openlocfilehash: 40efc256dde13d645d43f50bb574d73b5668919c
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703744"
---
# <a name="iclrmetahostgetversionfromfile-method"></a>ICLRMetaHost::GetVersionFromFile メソッド
ファイルパスを指定して、アセンブリの元の .NET Framework コンパイルバージョン (メタデータに格納されている) を取得します。 このメソッドは、 [GetFileVersion](getfileversion-function.md)関数よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetVersionFromFile (  
    [in] LPCWSTR pwzFilePath,  
    [out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
    [in, out] DWORD *pcchBuffer);  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzFilePath`  
 から完全なアセンブリファイルパス。  
  
 `pwzbuffer`  
 入出力メタデータに格納されている .NET Framework のコンパイルバージョン。 "v*A と*いう形式になります。*B*[.*X*] " *A*、 *B*、および*X*は、メジャーバージョン、マイナーバージョン、およびビルド番号に対応する10進数です。 この文字列の長さは MAX_PATH に制限されています。  
  
> [!NOTE]
> この出力は、C:\Windows\Microsoft.NET\Framework. の下に表示される .NET Framework バージョンのディレクトリ名と一致します。  
  
 値の例としては、"v v1.0.3705"、"v 1.1.4322"、"v v2.0.50727"、および "v4.0" があります。*X*"。ここで*x*は、インストールされているビルド番号に依存します。 "V" プレフィックスが必要であることに注意してください。  
  
 `pcchBuffer`  
 [入力、出力]`pwzbuffer`バッファーオーバーランを回避するためののサイズ。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pwzbuffer` または `pcchBuffer` が null です。|  
|HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)|バッファーが小さすぎます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRMetaHost インターフェイス](iclrmetahost-interface.md)
- [ホスティング](index.md)
