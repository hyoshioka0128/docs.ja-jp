---
title: CoreClrDebugRuntimeInfo 構造体
ms.date: 03/30/2017
api_name:
- CoreClrDebugRuntimeInfo
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- CoreClrDebugRuntimeInfo
helpviewer_keywords:
- remote debugging API [Silverlight]
- CoreDebugRuntimeInfo structure
- Silverlight, remote debugging
ms.assetid: bd01c30f-b7a8-4179-9497-622b6599b1a6
topic_type:
- apiref
ms.openlocfilehash: 2c41e7db32ee8557a6c03217b95fd5b040655c70
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860932"
---
# <a name="coreclrdebugruntimeinfo-structure"></a>CoreClrDebugRuntimeInfo 構造体
リモート コンピューター上のプロセスに読み込まれる共通言語ランタイム (CLR) インスタンスを表します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
struct  CoreClrDebugRuntimeInfo {  
    DWORD m_dwInternalID;  
};  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`m_dwInternalID`|対象のコンピューターで実行されているリモート デバッグ プロキシによって割り当てられたランタイム識別子。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Coreclrremoteデバッグインターフェイス .h  
  
 **Library:** mscordbi_macx86 .dll  
  
 **.NET Framework のバージョン:** 3.5 SP1
