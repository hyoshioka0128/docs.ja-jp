---
title: IMapToken::Map メソッド
ms.date: 03/30/2017
api_name:
- IMapToken.Map
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMapToken::Map
helpviewer_keywords:
- IMapToken::Map method [.NET Framework metadata]
- Map method [.NET Framework metadata]
ms.assetid: b9b4bf2f-1098-43d6-9619-a99b4bda1940
topic_type:
- apiref
ms.openlocfilehash: 027694cee1b3e4d990796ba31300918f6d859679
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008197"
---
# <a name="imaptokenmap-method"></a>IMapToken::Map メソッド
メタデータシグネチャを使用して、アセンブリ間のリレーションシップをマップします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Map (  
    [in]  mdToken tkImp,
    [in]  mdToken tkEmit  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tkImp`  
 からインポートされたコードオブジェクトを表すメタデータトークン。  
  
 `tkEmit`  
 から出力されたコードオブジェクトを表すメタデータトークン。  
  
## <a name="remarks"></a>コメント  
 マージ中にトークンの再マップが行われると、元のトークンはインポートされた (ソース) メタデータスコープ内でスコープが設定され、新しいトークンのスコープは、出力された (ターゲット) メタデータスコープに設定されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMapToken インターフェイス](imaptoken-interface.md)
