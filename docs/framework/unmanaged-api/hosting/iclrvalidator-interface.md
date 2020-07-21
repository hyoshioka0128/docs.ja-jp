---
title: ICLRValidator インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRValidator
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRValidator
helpviewer_keywords:
- ICLRValidator interface [.NET Framework hosting]
ms.assetid: 2edd0a10-77fb-4173-91eb-f2970cc364d0
topic_type:
- apiref
ms.openlocfilehash: e071f9cba7e991c59bf697647e0e4badea57573a
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762046"
---
# <a name="iclrvalidator-interface"></a>ICLRValidator インターフェイス
ポータブル実行可能 (PE) イメージを検証し、検証エラーを報告するためのメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[FormatEventInfo メソッド](iclrvalidator-formateventinfo-method.md)|指定された検証エラーに関する詳細メッセージを取得します。|  
|[Validate メソッド](iclrvalidator-validate-method.md)|指定したファイル内のポータブル実行可能ファイルまたは MSIL (Microsoft 中間言語) を検証します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** IValidator、IValidator  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRErrorReportingManager インターフェイス](iclrerrorreportingmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [CLRRuntimeHost コクラス](clrruntimehost-coclass.md)
