---
title: ICLRRuntimeHost::GetCLRControl メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.GetCLRControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::GetCLRControl
helpviewer_keywords:
- ICLRRuntimeHost::GetCLRControl method [.NET Framework hosting]
- GetCLRControl method [.NET Framework hosting]
ms.assetid: e47e3655-efd5-4572-a1dc-50c69bf2a468
topic_type:
- apiref
ms.openlocfilehash: 68bcdc33e34075cc5876ee721ef57282cdaa6e86
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703684"
---
# <a name="iclrruntimehostgetclrcontrol-method"></a>ICLRRuntimeHost::GetCLRControl メソッド
ホストが共通言語ランタイム (CLR) の側面をカスタマイズするために使用できる[ICLRControl interface](iclrcontrol-interface.md)型のインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCLRControl(  
    [out] ICLRControl** pCLRControl  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pCLRControl`  
 入出力ホストが CLR の追加の側面を構成できるようにする[ICLRControl interface](iclrcontrol-interface.md)型のインターフェイスポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetCLRControl`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_INVALIDOPERATION|CLR は既に開始されています。|  
  
## <a name="remarks"></a>解説  
 `ICLRControl`[Getclrmanager メソッド](iclrcontrol-getclrmanager-method.md)を提供します。このメソッドを使用すると、ホストは、マネージャーの型のいずれかへのインターフェイスポインターを取得できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
