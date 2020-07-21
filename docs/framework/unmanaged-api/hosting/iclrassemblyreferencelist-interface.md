---
title: ICLRAssemblyReferenceList インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRAssemblyReferenceList
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyReferenceList
helpviewer_keywords:
- ICLRAssemblyReferenceList interface [.NET Framework hosting]
ms.assetid: 5f890fdf-d22a-429e-a35f-135273d1a636
topic_type:
- apiref
ms.openlocfilehash: f1aa40ef868bf6ff7730e01ab66a6fec58af1196
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615879"
---
# <a name="iclrassemblyreferencelist-interface"></a>ICLRAssemblyReferenceList インターフェイス
ホストではなく、共通言語ランタイム (CLR) によって読み込まれるアセンブリの一覧を管理します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IsAssemblyReferenceInList メソッド](iclrassemblyreferencelist-isassemblyreferenceinlist-method.md)|指定されたポインターがリスト内のアセンブリを参照しているかどうかを示す値を取得します。|  
|[IsStringAssemblyReferenceInList メソッド](iclrassemblyreferencelist-isstringassemblyreferenceinlist-method.md)|指定された名前がリスト内のアセンブリの名前と一致するかどうかを示す値を取得します。|  
  
## <a name="remarks"></a>解説  
 [ICLRAssemblyIdentityManager:: GetCLRAssemblyReferenceList](iclrassemblyidentitymanager-getclrassemblyreferencelist-method.md)メソッドを呼び出して、のインスタンスへのポインターを取得 `ICLRAssemblyReferenceList` します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyIdentityManager インターフェイス](iclrassemblyidentitymanager-interface.md)
- [IHostAssemblyStore インターフェイス](ihostassemblystore-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
