---
title: ICLRProbingAssemblyEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRProbingAssemblyEnum
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRProbingAssemblyEnum
helpviewer_keywords:
- ICLRProbingAssemblyEnum interface [.NET Framework hosting]
ms.assetid: e7d3ccab-b0f0-4872-8935-0ed72920171b
topic_type:
- apiref
ms.openlocfilehash: e1e114070f39e75254fc1bc0f8c1bf3e4733d5a2
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703378"
---
# <a name="iclrprobingassemblyenum-interface"></a>ICLRProbingAssemblyEnum インターフェイス
共通言語ランタイム (CLR) の内部にあるアセンブリの id 情報を使用して、ホストがアセンブリのプローブ id を取得できるようにするメソッドを提供します。このメソッドは、その id を作成または理解する必要はありません。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Get メソッド](iclrprobingassemblyenum-get-method.md)|指定したインデックス位置にあるアセンブリ id を取得します。|  
  
## <a name="remarks"></a>解説  
 [ICLRAssemblyIdentityManager:: GetProbingAssembliesFromReference](iclrassemblyidentitymanager-getprobingassembliesfromreference-method.md)などのメソッドは、 `ICLRProbingAssemblyEnum` インスタンスを返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyIdentityManager インターフェイス](iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
