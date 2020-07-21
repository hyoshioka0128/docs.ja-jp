---
title: ICLRMetaHost::GetRuntime メソッド
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.GetRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::GetRuntime
helpviewer_keywords:
- GetRuntime method [.NET Framework hosting]
- ICLRMetaHost::GetRuntime method [.NET Framework hosting]
ms.assetid: a10749f1-ab91-47cf-982f-d8ccd2e81bd2
topic_type:
- apiref
ms.openlocfilehash: d482e25c7bf0f028e2478c8e7b7863bc54d7aeb9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504195"
---
# <a name="iclrmetahostgetruntime-method"></a>ICLRMetaHost::GetRuntime メソッド
共通言語ランタイム (CLR) の特定のバージョンに対応する[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)インターフェイスを取得します。 このメソッドは、 [STARTUP_LOADER_SAFEMODE](startup-flags-enumeration.md)フラグと共に使用される[Corbindtoruntimeex](corbindtoruntimeex-function.md)関数よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRuntime (  
    [in] LPCWSTR pwzVersion,  
    [in] REFIID riid,  
    [out,iid_is(riid), retval] LPVOID *ppRuntime  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzVersion`  
 からメタデータに格納されている .NET Framework のコンパイルバージョン。 "v*A と*いう形式になります。*B*[.*X*] " *A*、 *B*、および*X*は、メジャーバージョン、マイナーバージョン、およびビルド番号に対応する10進数です。  
  
> [!NOTE]
> このパラメーターは、C:\windows\ microsoft.net \framework または C:\Windows\Microsoft.NET\Framework64. の下に表示される .NET Framework バージョンのディレクトリ名と一致する必要があります。  
  
 値の例としては、"v v1.0.3705"、"v 1.1.4322"、"v v2.0.50727"、および "v4.0" があります。*X*"。ここで*x*は、インストールされているビルド番号に依存します。 "V" プレフィックスが必要です。  
  
 `riid`  
 から目的のインターフェイスの識別子。 現時点では、このパラメーターの有効な値は IID_ICLRRuntimeInfo のみです。  
  
 `ppRuntime`  
 入出力要求されたランタイムに対応する[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)インターフェイスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pwzVersion` または `ppRuntime` が null です。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、 [ICorRuntimeHost](icorruntimehost-interface.md)インターフェイスや、非推奨の関数などの従来の関数のようなレガシインターフェイスと常に相互作用し `CorBindTo*` ます (「.NET FRAMEWORK 2.0 ホスティング API の[非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)」を参照してください)。 つまり、レガシ API で読み込まれたランタイムは新しい API から参照でき、新しい API で読み込まれたランタイムはレガシ API から参照できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRMetaHost インターフェイス](iclrmetahost-interface.md)
- [非推奨の CLR のホスト インターフェイスおよびコクラス](deprecated-clr-hosting-interfaces-and-coclasses.md)
- [CLR ホスト インターフェイス](clr-hosting-interfaces.md)
- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
- [ホスティング](index.md)
