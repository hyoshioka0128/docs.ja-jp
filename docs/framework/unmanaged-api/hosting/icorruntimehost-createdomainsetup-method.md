---
title: ICorRuntimeHost::CreateDomainSetup メソッド
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateDomainSetup
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateDomainSetup
helpviewer_keywords:
- CreateDomainSetup method [.NET Framework hosting]
- ICorRuntimeHost::CreateDomainSetup method [.NET Framework hosting]
ms.assetid: c21dab60-fb65-47d9-8a94-7fd47ca53b48
topic_type:
- apiref
ms.openlocfilehash: aa1ce70311cd4ef0204c1c31efee8bd7b313c81d
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762332"
---
# <a name="icorruntimehostcreatedomainsetup-method"></a>ICorRuntimeHost::CreateDomainSetup メソッド
インスタンスへの IAppDomainSetup 型のインターフェイスポインターを取得し <xref:System.AppDomainSetup?displayProperty=nameWithType> ます。 `IAppDomainSetup`アプリケーションドメインを作成する前に構成するためのメソッドを提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateDomainSetup (  
    [out] IUnknown** pAppDomainSetup  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomainSetup`  
 入出力インスタンスへのインターフェイスポインター <xref:System.AppDomainSetup?displayProperty=nameWithType> 。 このパラメーターはとして型指定さ `IUnknown` れるため、通常、呼び出し元は `QueryInterface` このポインターを呼び出して、型のインターフェイスポインターを取得する必要があり `IAppDomainSetup` ます。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|操作に成功しました。|  
|S_FALSE|操作を完了できませんでした。|  
|E_FAIL|不明な重大なエラーが発生しました。 メソッドが E_FAIL を返す場合、このプロセスでは共通言語ランタイム (CLR) は使用できなくなります。 後続のホスト Api への呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
  
## <a name="remarks"></a>解説  
 このメソッドから返されるポインターは、通常、パラメーターとして[Createdomainex](icorruntimehost-createdomainex-method.md)メソッドに渡されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework バージョン:** 1.0、1.1  
  
## <a name="see-also"></a>関連項目

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- <xref:System.AppDomainSetup>
- <xref:System.IAppDomainSetup?displayProperty=nameWithType>
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
