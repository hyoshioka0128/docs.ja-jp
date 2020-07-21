---
title: ICLRRuntimeInfo::IsLoadable メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.IsLoadable
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::IsLoadable
helpviewer_keywords:
- IsLoadable method [.NET Framework hosting]
- ICLRRuntimeInfo::IsLoadable method [.NET Framework hosting]
ms.assetid: 205ca53b-e78e-49b2-9a46-2a7823e96b8c
topic_type:
- apiref
ms.openlocfilehash: a1cd169fc4be5b1dd3ab1a83f4ad143ba2e2442b
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007365"
---
# <a name="iclrruntimeinfoisloadable-method"></a>ICLRRuntimeInfo::IsLoadable メソッド
このインターフェイスに関連付けられているランタイムを現在のプロセスに読み込むことができるかどうかを示します。プロセスに既に読み込まれている可能性のある他のランタイムを考慮してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsLoadable(  
        [out, retval] BOOL *pbLoadable);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbLoadable`  
 [出力] `true`このランタイムを現在のプロセスに読み込むことができる場合は。それ以外の場合は `false` 。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pbLoadable` が null です。|  
  
## <a name="remarks"></a>コメント  
 別のランタイムが既にプロセスに読み込まれていて、このインターフェイスに関連付けられているランタイムをインプロセス side-by-side 実行用に読み込むことができる場合、はを `pbLoadable` 返し `true` ます。 2つのランタイムをインプロセスで並列実行できない場合、はを `pbLoadable` 返し `false` ます。 たとえば、共通言語ランタイム (CLR) バージョン4は、CLR バージョン2.0 または CLR バージョン1.1 と同じプロセスでサイドバイサイドで実行できます。 ただし、CLR バージョン1.1 と CLR バージョン2.0 をインプロセスで並列実行することはできません。  
  
 プロセスにランタイムが読み込まれていない場合、このメソッドは常にを返し `true` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
