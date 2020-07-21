---
title: InitDbgTransportManager 関数
ms.date: 03/30/2017
api_name:
- InitDbgTransportManager
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- InitDbgTransportManager
helpviewer_keywords:
- remote debugging API [Silverlight]
- InitDbgTransportManager function
- Silverlight, remote debugging
ms.assetid: a30102ff-c52e-48c9-b3a9-aa14286a42b2
topic_type:
- apiref
ms.openlocfilehash: e18ceb25b9c58a9710ef967cb071e3ef55beea8c
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421047"
---
# <a name="initdbgtransportmanager-function"></a>InitDbgTransportManager 関数
プロセスおよびランタイムの列挙のためにリモート ターゲットに接続するよう、トランスポート マネージャーを初期化します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT InitDbgTransportManager ();  
```  
  
## <a name="return-value"></a>戻り値  
 S_OK  
 成功しました。  
  
 E_OUTOFMEMORY  
 関数はトランスポート マネージャーにメモリを割り当てられませんでした。  
  
 E_FAIL (またはその他の E_ リターン コード)  
 その他のエラーが発生しました。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Coreclrremoteデバッグインターフェイス .h  
  
 **Library:** mscordbi_macx86 .dll  
  
 **.NET Framework のバージョン:** 3.5 SP1
