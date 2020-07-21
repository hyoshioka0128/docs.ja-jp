---
title: ICorPublish インターフェイス
ms.date: 03/30/2017
api_name:
- ICorPublish
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish
helpviewer_keywords:
- ICorPublish interface [.NET Framework debugging]
ms.assetid: 87c4fcb2-7703-4a2e-afb6-42973381b960
topic_type:
- apiref
ms.openlocfilehash: 1bd2f537cfa6a27c24ba91ea7caa29dc9e71a74e
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396320"
---
# <a name="icorpublish-interface"></a>ICorPublish インターフェイス
プロセスに関する情報、およびそれらのプロセス内のアプリケーションドメインに関する情報を公開するための一般的なインターフェイスとして機能します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumProcesses メソッド](icorpublish-enumprocesses-method.md)|このコンピューター上で実行されているマネージプロセスを含む[ICorPublishProcessEnum](icorpublishprocessenum-interface.md)インスタンスを取得します。|  
|[GetProcess メソッド](icorpublish-getprocess-method.md)|指定した識別子を持つプロセスを表す[ICorPublishProcess](icorpublishprocess-interface.md)インスタンスを取得します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [CorpubPublish コクラス](corpubpublish-coclass.md)
