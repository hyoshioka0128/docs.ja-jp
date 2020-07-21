---
title: ICorRuntimeHost::CloseEnum メソッド
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CloseEnum
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CloseEnum
helpviewer_keywords:
- CloseEnum method, ICorRuntimeHost interface [.NET Framework hosting]
- ICorRuntimeHost::CloseEnum method [.NET Framework hosting]
ms.assetid: f7ce7e8c-0a3e-4587-a180-063e2b85940e
topic_type:
- apiref
ms.openlocfilehash: a5a86df3ac1f50ca624490ad80a6fed903433436
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762371"
---
# <a name="icorruntimehostcloseenum-method"></a>ICorRuntimeHost::CloseEnum メソッド
ドメイン列挙子をドメインリストの先頭にリセットします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CloseEnum (  
    [in] HCORENUM hEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hEnum`  
 からリセットする列挙子。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|操作に成功しました。|  
|S_FALSE|操作を完了できませんでした。|  
|E_FAIL|不明な重大なエラーが発生しました。 メソッドが E_FAIL を返す場合、このプロセスでは共通言語ランタイム (CLR) は使用できなくなります。 後続のホスト Api への呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** 1.0、1.1  
  
## <a name="see-also"></a>関連項目

- [CorBindToRuntimeEx 関数](corbindtoruntimeex-function.md)
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
