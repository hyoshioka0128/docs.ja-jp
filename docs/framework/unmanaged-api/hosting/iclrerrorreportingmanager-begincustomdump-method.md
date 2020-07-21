---
title: ICLRErrorReportingManager::BeginCustomDump メソッド
ms.date: 03/30/2017
api_name:
- ICLRErrorReportingManager.BeginCustomDump
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRErrorReportingManager::BeginCustomDump
helpviewer_keywords:
- ICLRErrorReportingManager::BeginCustomDump method [.NET Framework hosting]
- BeginCustomDump method
ms.assetid: 93424a87-ba13-4fa1-b4dc-69d44437b7ae
topic_type:
- apiref
ms.openlocfilehash: 4c83ffaf920abe005ba987e0a744e13aa0d3c016
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615671"
---
# <a name="iclrerrorreportingmanagerbegincustomdump-method"></a>ICLRErrorReportingManager::BeginCustomDump メソッド
エラー報告のためのカスタムヒープダンプの構成を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT BeginCustomDump (  
    [in] ECustomDumpFlavor dwFlavor,  
    [in] DWORD dwNumItems,  
    [in, size_is(dwNumItems), length_is(dwNumItems)] CustomDumpItem items[],  
    DWORD dwReserved  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwFlavor`  
 からカスタムヒープダンプを構築するときに使用するヒープダンプの種類を示す[ECustomDumpFlavor](ecustomdumpflavor-enumeration.md)値です。  
  
 `dwNumItems`  
 から配列の長さ `items` 。 `dwFlavor`が DUMP_FLAVOR_Mini でない場合は、を `dwNumItems` 0 にする必要があります。  
  
 `items`  
 からミニダンプに追加する項目を指定する、 [Customdumpitem](customdumpitem-structure.md)インスタンスの配列。 `dwFlavor`が DUMP_FLAVOR_Mini でない場合は、を `items` null にする必要があります。  
  
 `dwReserved`  
 から将来使用するために予約されています。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 メソッドは、 `BeginCustomDump` カスタムヒープダンプ構成を設定します。 [Endcustomdump](iclrerrorreportingmanager-endcustomdump-method.md)メソッドは、カスタムヒープダンプ構成をクリアし、関連付けられているすべての状態を解放します。 カスタムヒープダンプの完了後に呼び出す必要があります。  
  
> [!IMPORTANT]
> を呼び出さない `EndCustomDump` と、メモリがリークします。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [CustomDumpItem 構造体](customdumpitem-structure.md)
- [ECustomDumpFlavor 列挙型](ecustomdumpflavor-enumeration.md)
- [ICLRErrorReportingManager インターフェイス](iclrerrorreportingmanager-interface.md)
