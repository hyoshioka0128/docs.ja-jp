---
title: IHostIoCompletionManager::GetHostOverlappedSize メソッド
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.GetHostOverlappedSize
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::GetHostOverlappedSize
helpviewer_keywords:
- IHostIoCompletionManager::GetHostOverlappedSize method [.NET Framework hosting]
- GetHostOverlappedSize method [.NET Framework hosting]
ms.assetid: 2902578b-d5e2-4f8d-a103-0c7b6dceda9e
topic_type:
- apiref
ms.openlocfilehash: a97009a4ebc834d867dddcc350033c550364ea42
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804743"
---
# <a name="ihostiocompletionmanagergethostoverlappedsize-method"></a>IHostIoCompletionManager::GetHostOverlappedSize メソッド
ホストが i/o 要求に追加しようとしているカスタムデータのサイズを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHostOverlappedSize (  
    [out] DWORD *pcbSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pcbSize`  
 入出力Win32 オブジェクトのサイズに加えて、共通言語ランタイム (CLR: common language runtime) によって割り当てられるバイト数へのポインター `OVERLAPPED` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetHostOverlappedSize`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 Windows プラットフォーム Api に対するすべての非同期 i/o 呼び出しは、 `OVERLAPPED` ファイルポインターの位置などの情報を提供する Win32 オブジェクトを受け取ります。 状態を維持するために、非同期 i/o 呼び出しを行うアプリケーションは、通常、カスタムデータを構造に追加します。 `GetHostOverlappedSize`と[Iho、O補完 manager:: InitializeHostOverlapped](ihostiocompletionmanager-initializehostoverlapped-method.md)は、このようなカスタムデータをホストに含める機会を提供します。  
  
 CLR は、メソッドを呼び出して、 `GetHostOverlappedSize` ホストがオブジェクトに追加するカスタムデータのサイズを決定し `OVERLAPPED` ます。  
  
> [!NOTE]
> `GetHostOverlappedSize`は1回だけ呼び出されます。 ホストのカスタムデータは、すべての i/o 要求に対して同じサイズである必要があります。  
  
> [!IMPORTANT]
> オブジェクト自体のサイズ `OVERLAPPED` は、の値には含まれません `pcbSize` 。  
  
 構造体の詳細については、 `OVERLAPPED` Windows プラットフォームのドキュメントを参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.NativeOverlapped>
- [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)
- [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)
