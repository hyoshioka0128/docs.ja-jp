---
title: ICorRuntimeHost::CreateDomainEx メソッド
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateDomainEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateDomainEx
helpviewer_keywords:
- ICorRuntimeHost::CreateDomainEx method [.NET Framework hosting]
- CreateDomainEx method [.NET Framework hosting]
ms.assetid: 1bdde382-f8ba-4cc8-94b2-d1ac919c585e
topic_type:
- apiref
ms.openlocfilehash: 4e5856fbcda83c1dd30559c6f59f63495faea78d
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762345"
---
# <a name="icorruntimehostcreatedomainex-method"></a>ICorRuntimeHost::CreateDomainEx メソッド
アプリケーションドメインを作成します。 呼び出し元は、型のインターフェイスポインターを <xref:System._AppDomain> 型のインスタンスに受信し <xref:System.AppDomain?displayProperty=nameWithType> ます。 このメソッドを使用すると、呼び出し元は IAppDomainSetup インスタンスを渡して、返されたインスタンスの追加の機能を構成でき <xref:System._AppDomain> ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateDomainEx (  
    [in] LPCWSTR     pwzFriendlyName,  
    [in] IUnknown*   pSetup,  
    [in] IUnknown*   pIdentityArray,  
    [out] IUnknown** pAppDomain  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzFriendlyName`  
 からドメインのフレンドリ名を指定するために使用される省略可能なパラメーター。 このフレンドリ名は、ドメインを識別するためのデバッガーなどのユーザーインターフェイスに表示できます。  
  
 `pSetup`  
 から`IAppDomainSetup` [ICorRuntimeHost:: CreateDomainSetup](icorruntimehost-createdomainsetup-method.md)メソッドの呼び出しによって取得される、型の省略可能なインターフェイスポインター。  
  
 `pIdentityArray`  
 から`IIdentity`アクセス許可セットを確立するためにセキュリティポリシーによってマップされた証拠を表す、インスタンスへのポインターの配列 (省略可能)。 `IIdentity`オブジェクトは、 [createevidence](icorruntimehost-createevidence-method.md)メソッドを呼び出すことによって取得できます。  
  
 `pAppDomain`  
 入出力<xref:System._AppDomain> <xref:System.AppDomain?displayProperty=nameWithType> ドメインをさらに制御するために使用できるのインスタンスへの型のインターフェイスポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|操作に成功しました。|  
|S_FALSE|操作を完了できませんでした。|  
|E_FAIL|不明な重大なエラーが発生しました。 メソッドが E_FAIL を返す場合、このプロセスでは共通言語ランタイム (CLR) は使用できなくなります。 後続のホスト Api への呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
  
## <a name="remarks"></a>解説  
 `CreateDomainEx`は、呼び出し元がインスタンスにアプリケーションドメインを構成するためのプロパティ値を渡すことができるようにすることで、 [Createdomain](icorruntimehost-createdomain-method.md)の機能を拡張し `IAppDomainSetup` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework バージョン:** 1.0、1.1  
  
## <a name="see-also"></a>関連項目

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- <xref:System.IAppDomainSetup?displayProperty=nameWithType>
- [CreateDomain メソッド](icorruntimehost-createdomain-method.md)
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
