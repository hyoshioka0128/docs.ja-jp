---
title: IAssemblyCacheItem::Commit メソッド
ms.date: 03/30/2017
api_name:
- IAssemblyCacheItem.Commit
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCacheItem::Commit
helpviewer_keywords:
- IAssemblyCacheItem::Commit method [.NET Framework fusion]
- Commit method, IAssemblyCacheItem interface [.NET Framework fusion]
ms.assetid: c2321f17-f46f-4815-ae41-b28678753613
topic_type:
- apiref
ms.openlocfilehash: f840438e175790a2b4c97302963b910f98dffb7d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176566"
---
# <a name="iassemblycacheitemcommit-method"></a>IAssemblyCacheItem::Commit メソッド
キャッシュされたアセンブリ参照をメモリにコミットします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Commit (  
    [in] DWORD dwFlags,
    [out, optional] ULONG *pulDisposition  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwFlags`  
 [in]Fusion.idl で定義されているフラグ。  
  
 `pulDisposition`  
 [アウト、オプション]操作の結果を示す値。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** フュージョン.h  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IAssemblyCacheItem インターフェイス](iassemblycacheitem-interface.md)
