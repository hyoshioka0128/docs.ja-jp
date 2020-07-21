---
title: CLRCreateInstance 関数
ms.date: 03/30/2017
api_name:
- CLRCreateInstance
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- COM
f1_keywords:
- CLRCreateInstance
helpviewer_keywords:
- CLRCreateInstance function [.NET Framework hosting]
ms.assetid: 5de13327-96c6-4697-a89e-b8bf40717855
topic_type:
- apiref
ms.openlocfilehash: 4aeacc718632c133550ed8de6649716c5d8b7423
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504445"
---
# <a name="clrcreateinstance-function"></a>CLRCreateInstance 関数
には、 [ICLRMetaHost](iclrmetahost-interface.md)、 [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)、または[ICLRDebugging](../debugging/iclrdebugging-interface.md)の3つのインターフェイスのいずれかが用意されています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CLRCreateInstance(  
    [in]  REFCLSID  clsid,  
    [in]  REFIID     riid,  
    [out] LPVOID  * ppInterface  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `clsid`  
 からCLSID_CLRMetaHost、CLSID_CLRMetaHostPolicy、または CLSID_CLRDebugging の3つのクラス識別子のいずれか。  
  
 `riid`  
 から3つのインターフェイス識別子 (Iid が) のいずれか。 IID_ICLRMetaHost、IID_ICLRMetaHostPolicy、または IID_ICLRDebugging です。  
  
 `ppInterface`  
 入出力[ICLRMetaHost](iclrmetahost-interface.md)、 [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)、または[ICLRDebugging](../debugging/iclrdebugging-interface.md)の3つのインターフェイスのいずれか。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`ppInterface` が null です。|  
  
## <a name="remarks"></a>解説  
 次の表は、とでサポートされている組み合わせを示して `clsid` `riid` います。  
  
|`clsid`|`riid`|  
|--------------|------------|  
|CLSID_CLRMetaHost|IID_ICLRMetaHost|  
|CLSID_CLRMetaHostPolicy|IID_ICLRMetaHostPolicy|  
|CLSID_CLRDebugging|IID_ICLRDebugging|  
  
 次のコードは、を使用して3つすべてのインターフェイスを取得する方法を示してい `CLRCreateInstance` ます。  
  
```cpp  
#include <metahost.h>  
#pragma comment(lib, "mscoree.lib")  
  
ICLRMetaHost       *pMetaHost       = NULL;  
ICLRMetaHostPolicy *pMetaHostPolicy = NULL;  
ICLRDebugging      *pCLRDebugging   = NULL;  
HRESULT hr;  
hr = CLRCreateInstance(CLSID_CLRMetaHost, IID_ICLRMetaHost,  
                    (LPVOID*)&pMetaHost);  
hr = CLRCreateInstance (CLSID_CLRMetaHostPolicy, IID_ICLRMetaHostPolicy,  
                    (LPVOID*)&pMetaHostPolicy);  
hr = CLRCreateInstance (CLSID_CLRDebugging, IID_ICLRDebugging,  
                    (LPVOID*)&pCLRDebugging);  
```  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティング](index.md)
