---
title: ICLRErrorReportingManager::EndCustomDump メソッド
ms.date: 03/30/2017
api_name:
- ICLRErrorReportingManager.EndCustomDump
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRErrorReportingManager::EndCustomDump
helpviewer_keywords:
- ICLRErrorReportingManager::EndCustomDump method [.NET Framework hosting]
- EndCustomDump method [.NET Framework hosting]
ms.assetid: 88a5da04-8729-4108-82c4-af206a7d483e
topic_type:
- apiref
ms.openlocfilehash: 704d8d0921e671e4172fa6e0ae3f14c4908f289a
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615658"
---
# <a name="iclrerrorreportingmanagerendcustomdump-method"></a>ICLRErrorReportingManager::EndCustomDump メソッド
[ICLRErrorReportingManager:: BeginCustomDump](iclrerrorreportingmanager-begincustomdump-method.md)メソッドの以前の呼び出しで指定されたカスタムスタックダンプ構成を削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EndCustomDump ();  
```  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`EndCustomDump`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 メソッドは、 `EndCustomDump` メソッドの以前の呼び出しによって設定されたカスタムスタックダンプ構成をクリア `BeginCustomDump` し、関連付けられているすべての状態を解放します。 カスタムスタックダンプの完了後に呼び出す必要があります。  
  
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
