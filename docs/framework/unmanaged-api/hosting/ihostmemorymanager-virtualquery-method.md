---
title: IHostMemoryManager::VirtualQuery メソッド
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualQuery
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualQuery
helpviewer_keywords:
- IHostMemoryManager::VirtualQuery method [.NET Framework hosting]
- VirtualQuery method [.NET Framework hosting]
ms.assetid: 757af1e6-b9e8-49e7-b5db-342be3aa205f
topic_type:
- apiref
ms.openlocfilehash: 71c56b5dab2409be05e8260b1a2e39d28a709bba
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804378"
---
# <a name="ihostmemorymanagervirtualquery-method"></a>IHostMemoryManager::VirtualQuery メソッド
対応する Win32 関数の論理ラッパーとして機能します。 の Win32 実装では、 `VirtualQuery` 呼び出し元プロセスの仮想アドレス空間にあるページの範囲に関する情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT VirtualQuery (  
    [in]  void*    lpAddress,  
    [out] void*    lpBuffer,  
    [in]  SIZE_T   dwLength,  
    [out] SIZE_T*  pResult  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `lpAddress`  
 から照会される仮想メモリ内のアドレスへのポインター。  
  
 `lpBuffer`  
 入出力指定されたメモリ領域に関する情報を格納している構造体へのポインター。  
  
 `dwLength`  
 からが指すバッファーのサイズ (バイト単位) `lpBuffer` 。  
  
 `pResult`  
 入出力情報バッファーによって返されたバイト数へのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`VirtualQuery`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `VirtualQuery`呼び出しプロセスの仮想アドレス空間にあるページの範囲に関する情報を提供します。 この実装は、パラメーターの値を、 `pResult` 情報バッファーで返されるバイト数に設定し、HRESULT 値を返します。 Win32 関数で `VirtualQuery` は、戻り値はバッファーサイズです。 詳細については、Windows プラットフォームのドキュメントを参照してください。  
  
> [!IMPORTANT]
> のオペレーティングシステムの実装で `VirtualQuery` は、デッドロックは発生せず、ユーザーコード内で中断されたランダムスレッドで完了まで実行できます。 このメソッドのホストされたバージョンを実装する場合は、細心の注意を払ってください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
