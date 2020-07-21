---
title: ICorPublishProcess::IsManaged メソッド
ms.date: 03/30/2017
api_name:
- ICorPublishProcess.IsManaged
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcess::IsManaged
helpviewer_keywords:
- IsManaged method, ICorPublishProcess interface [.NET Framework debugging]
- ICorPublishProcess::IsManaged method [.NET Framework debugging]
ms.assetid: 06b1f7cc-acdf-47a6-9d53-d9dec2424152
topic_type:
- apiref
ms.openlocfilehash: 3eec84624866b2be7068d7875cd650828c283fd2
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421099"
---
# <a name="icorpublishprocessismanaged-method"></a>ICorPublishProcess::IsManaged メソッド
この[ICorPublishProcess](icorpublishprocess-interface.md)によって参照されるプロセスに、マネージコードがあることがわかっているかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsManaged (  
    [out] BOOL   *pbManaged  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbManaged`  
 入出力プロセスにマネージコードがあるかどうかを示すブール値へのポインター。 `true`プロセスにマネージコードがある場合は、値はです。それ以外の場合は `false` です。  
  
## <a name="remarks"></a>解説  
 現在のバージョンのでは `ICorPublishProcess` 、マネージコードを持つプロセスのみにアクセスが許可されるため、は `IsManaged` 常にを返し `true` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublishProcess インターフェイス](icorpublishprocess-interface.md)
