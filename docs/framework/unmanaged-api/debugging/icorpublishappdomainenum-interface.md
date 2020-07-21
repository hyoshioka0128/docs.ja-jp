---
title: ICorPublishAppDomainEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorPublishAppDomainEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishAppDomainEnum
helpviewer_keywords:
- ICorPublishAppDomainEnum interface [.NET Framework debugging]
ms.assetid: bb798c56-042e-475d-a245-b6fac36d0c07
topic_type:
- apiref
ms.openlocfilehash: a48e20413f466e25a9145e9dbf1ba93d90155770
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397038"
---
# <a name="icorpublishappdomainenum-interface"></a>ICorPublishAppDomainEnum インターフェイス
プロセス内に現在存在する[ICorPublishAppDomain](icorpublishappdomain-interface.md)オブジェクトのコレクションを走査するメソッドを提供する[ICorPublishEnum](icorpublishenum-interface.md)インターフェイスのサブクラス。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Next メソッド](icorpublishappdomainenum-next-method.md)|現在の位置から開始して、指定した数の `ICorPublishAppDomain` インスタンスをコレクションから取得します。|  
  
## <a name="remarks"></a>解説  
 インターフェイスは、 `ICorPublishAppDomainEnum` 抽象インターフェイス[ICorPublishEnum](icorpublishenum-interface.md)のメソッドを実装します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [CorpubPublish コクラス](corpubpublish-coclass.md)
