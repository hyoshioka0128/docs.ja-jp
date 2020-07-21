---
title: CorLaunchApplication 関数
ms.date: 03/30/2017
api_name:
- CorLaunchApplication
api_location:
- mscoree.dll
- clr.dll
api_type:
- COM
f1_keywords:
- CorLaunchApplication
helpviewer_keywords:
- CorLaunchApplication function [.NET Framework hosting]
ms.assetid: 71f362a9-8fe2-47ce-9302-05a645cf3d7d
topic_type:
- apiref
ms.openlocfilehash: 031bfc3d7fcd9f1f04e616e460cb3201813eae55
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616555"
---
# <a name="corlaunchapplication-function"></a>CorLaunchApplication 関数
指定したネットワーク パスのアプリケーションを、指定したマニフェストとその他のアプリケーション データを使用して起動します。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CorLaunchApplication (  
    [in]  HOST_TYPE                dwClickOnceHost,  
    [in]  LPCWSTR                  pwzAppFullName,  
    [in]  DWORD                    dwManifestPaths,  
    [in]  LPCWSTR                 *ppwzManifestPaths,  
    [in]  DWORD                    dwActivationData,  
    [in]  LPCWSTR                 *ppwzActivationData,  
    [out] LPPROCESS_INFORMATION    lpProcessInformation  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwClickOnceHost`  
 からアプリケーションを起動しているホストの種類を指定する[HOST_TYPE](host-type-enumeration.md)列挙体の値。  
  
 `pwzAppFullName`  
 から起動されるアプリケーションの完全な名前。  
  
 `dwManifestPaths`  
 からアプリケーションのマニフェストパスの数。  
  
 `ppwzManifestPaths`  
 から文字列の配列。それぞれが、起動されるアプリケーションのマニフェストへのパスを指定します。  
  
 `dwActivationData`  
 から起動されるアプリケーションのアクティブ化データ項目の数。  
  
 `ppwzActivationData`  
 から文字列の配列。各文字列は、起動されるアプリケーションのアクティベーションデータ項目です。  
  
 `lpProcessInformation`  
 入出力アプリケーションが読み込まれたプロセスに関する情報へのポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
