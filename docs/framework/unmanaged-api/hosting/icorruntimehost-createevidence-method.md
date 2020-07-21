---
title: ICorRuntimeHost::CreateEvidence メソッド
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateEvidence
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateEvidence
helpviewer_keywords:
- CreateEvidence method [.NET Framework hosting]
- ICorRuntimeHost::CreateEvidence method [.NET Framework hosting]
ms.assetid: e235ea80-b84c-4442-a4c3-fc96c25a8eb9
topic_type:
- apiref
ms.openlocfilehash: 264f16fc9e767584229376e67f5aee6db1069025
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501613"
---
# <a name="icorruntimehostcreateevidence-method"></a>ICorRuntimeHost::CreateEvidence メソッド
型のインターフェイスポインターを取得し <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType> ます。これにより、ホストは、 [createdomain](icorruntimehost-createdomain-method.md)メソッドまたは[createdomainex](icorruntimehost-createdomainex-method.md)メソッドに渡すセキュリティ証拠を作成できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateEvidence (  
    [out] IUnknown** pEvidence  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pEvidence`  
 入出力<xref:System.Security.Principal.IIdentity?displayProperty=nameWithType>セキュリティ証拠の作成に使用されるインスタンスへのインターフェイスポインター。 このポインターは型指定され `IUnknown` ているため、呼び出し元はへのポインターを取得するために、通常、このインターフェイスでを呼び出す必要があり `QueryInterface` <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType> ます。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|操作に成功しました。|  
|S_FALSE|操作を完了できませんでした。|  
|E_FAIL|不明な重大なエラーが発生しました。 メソッドが E_FAIL を返す場合、このプロセスでは共通言語ランタイム (CLR) は使用できなくなります。 後続のホスト Api への呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、ネイティブコードから設定できない空のコレクションを返します。 代わりに、メソッドを使用する必要があり <xref:System.Security.Policy.Evidence> ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework バージョン:** 1.0、1.1  
  
## <a name="see-also"></a>関連項目

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
