---
title: IHostSecurityManager::OpenThreadToken メソッド
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.OpenThreadToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::OpenThreadToken
helpviewer_keywords:
- IHostSecurityManager::OpenThreadToken method [.NET Framework hosting]
- OpenThreadToken method [.NET Framework hosting]
ms.assetid: d5999052-8bf0-4a9e-8621-da6284406b18
topic_type:
- apiref
ms.openlocfilehash: 85c7308f794929d753b50f58f69168f67a31cb85
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83803874"
---
# <a name="ihostsecuritymanageropenthreadtoken-method"></a>IHostSecurityManager::OpenThreadToken メソッド
現在実行中のスレッドに関連付けられている随意アクセストークンを開きます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OpenThreadToken (  
    [in]  DWORD    dwDesiredAccess,
    [in]  BOOL     bOpenAsSelf,
    [out] HANDLE   *phThreadToken  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwDesiredAccess`  
 からスレッドトークンへの要求されたアクセスの種類を指定するアクセス値のマスク。 これらの値は、Win32 関数で定義されてい `OpenThreadToken` ます。 要求されたアクセスの種類は、付与または拒否するアクセスの種類を決定するために、トークンの随意アクセス制御リスト (DACL) に対して調整されます。  
  
 `bOpenAsSelf`  
 [入力] `true`呼び出し元スレッドのプロセスのセキュリティコンテキストを使用してアクセスチェックを行うように指定する場合は。`false`呼び出し元スレッドのセキュリティコンテキストを使用してアクセスチェックを実行するように指定する場合は。 スレッドがクライアントを偽装している場合は、クライアントプロセスのセキュリティコンテキストになります。  
  
 `phThreadToken`  
 入出力新しく開かれたアクセストークンへのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`OpenThreadToken`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `IHostSecurityManager::OpenThreadToken`は、同じ名前の対応する Win32 関数と同じように動作します。ただし、Win32 関数では、呼び出し元が任意のスレッドへのハンドルを渡すことを許可し、 `IHostSecurityManager::OpenThreadToken` は呼び出し元のスレッドに関連付けられたトークンのみを開くことができます。  
  
 `HANDLE`この型は COM に準拠していません。つまり、そのサイズはオペレーティングシステムに固有であり、カスタムマーシャリングが必要です。 したがって、このトークンは、CLR とホストの間でプロセス内でのみ使用されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostSecurityContext インターフェイス](ihostsecuritycontext-interface.md)
- [IHostSecurityManager インターフェイス](ihostsecuritymanager-interface.md)
