---
title: ICorRuntimeHost::NextDomain メソッド
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.NextDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::NextDomain
helpviewer_keywords:
- ICorRuntimeHost::NextDomain method [.NET Framework hosting]
- NextDomain method [.NET Framework hosting]
ms.assetid: fe07a05b-f6d6-44b5-ab01-b9a6eb15c350
topic_type:
- apiref
ms.openlocfilehash: 079164d15141983711e976e0209cc22c818d9cd9
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83760421"
---
# <a name="icorruntimehostnextdomain-method"></a>ICorRuntimeHost::NextDomain メソッド
列挙体の次のドメインへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT NextDomain (  
    [in] HCORENUM hEnum,  
    [out] void** pAppDomain  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hEnum`  
 から[Enumdomains](icorruntimehost-enumdomains-method.md)の呼び出しによって取得された列挙子。  
  
 `pAppDomain`  
 入出力列挙体の次のドメインを表す型へのインターフェイスポインター <xref:System._AppDomain?displayProperty=nameWithType> 。または、他のドメインが存在しない場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|操作に成功しました。|  
|S_FALSE|操作を完了できなかったか、列挙にドメインがありません。|  
|E_FAIL|不明な重大なエラーが発生しました。 メソッドが E_FAIL を返す場合、このプロセスでは共通言語ランタイム (CLR) は使用できなくなります。 後続のホスト Api への呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** 1.0、1.1  
  
## <a name="see-also"></a>関連項目

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
