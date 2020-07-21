---
title: CorBindToCurrentRuntime 関数
ms.date: 03/30/2017
api_name:
- CorBindToCurrentRuntime
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- HeaderDef
f1_keywords:
- CorBindToCurrentRuntime
helpviewer_keywords:
- CorBindToCurrentRuntime function [.NET Framework hosting]
ms.assetid: 6105c13e-d9cd-44d2-a95a-924e042830c7
topic_type:
- apiref
ms.openlocfilehash: 4c015d77deb4e6ed3d43074f2903e26b687de84f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493566"
---
# <a name="corbindtocurrentruntime-function"></a>CorBindToCurrentRuntime 関数
XML ファイルに格納されているバージョン情報を使用して、共通言語ランタイム (CLR: Common Language Runtime) をプロセスに読み込みます。 XML ファイルの形式は、標準のアプリケーション構成ファイルの後にモデル化されています。 構成ファイルの詳細については、「[構成ファイル スキーマ](../../configure-apps/file-schema/index.md)」を参照してください。  
  
 この関数は .NET Framework 4 で非推奨とされました。 「[プロセスへの共通言語ランタイムの読み込み](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/01918c6x(v=vs.100))」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CorBindToCurrentRuntime (  
    [in]  LPCWSTR   pwszFileName,  
    [in]  REFCLSID  rclsid,  
    [in]  REFIID    riid,  
    [out] LPVOID    *ppv  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwszFileName`  
 から読み込む CLR のバージョンを指定するアプリケーション構成ファイルの名前。 ファイル名が完全修飾されていない場合は、呼び出しを行った実行可能ファイルと同じディレクトリに存在すると見なされます。  
  
 読み込むランタイムのバージョンは、構成ファイルの要素の version 属性によって記述され [\<requiredRuntime>](../../configure-apps/file-schema/startup/requiredruntime-element.md) ます。  
  
 バージョンが指定されていない場合、または要素が見つからない場合は、 `<requiredRuntime>` コンピューターにインストールされている最新バージョンの CLR が読み込まれます。  
  
 `rclsid`  
 から`CLSID` [ICorRuntimeHost](icorruntimehost-interface.md)または[ICLRRuntimeHost](iclrruntimehost-interface.md)のいずれかのインターフェイスを実装するコクラスの。 サポートされている値は CLSID_CorRuntimeHost と CLSID_CLRRuntimeHost です。  
  
 `riid`  
 [入力] 要求するインターフェイスの `IID`。 サポートされている値は IID_ICorRuntimeHost と IID_ICLRRuntimeHost です。  
  
 `ppv`  
 入出力返されたインターフェイスポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [CorBindToRuntime 関数](corbindtoruntime-function.md)
- [CorBindToRuntimeByCfg 関数](corbindtoruntimebycfg-function.md)
- [CorBindToRuntimeEx 関数](corbindtoruntimeex-function.md)
- [CorBindToRuntimeHost 関数](corbindtoruntimehost-function.md)
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
