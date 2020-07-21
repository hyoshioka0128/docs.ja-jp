---
title: ICorDebugThread2::GetConnectionID メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetConnectionID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetConnectionID
helpviewer_keywords:
- ICorDebugThread2::GetConnectionID method [.NET Framework debugging]
- GetConnectionID method [.NET Framework debugging]
ms.assetid: 9c76b587-f941-4fa1-8b86-f3494fb10c8e
topic_type:
- apiref
ms.openlocfilehash: c630daa50d465622c421381ac080eaa8d9d8d01d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379076"
---
# <a name="icordebugthread2getconnectionid-method"></a>ICorDebugThread2::GetConnectionID メソッド
この ICorDebugThread2 オブジェクトの接続識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetConnectionID (  
    [out] CONNID *pdwConnectionId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pdwConnectionId`  
 入出力`CONNID`接続識別子を表す。  
  
## <a name="remarks"></a>Remarks  
 `GetConnectionID` `pdwConnectionId` このスレッドが接続の一部でない場合、このメソッドはパラメーターで0を返します。  
  
 このスレッドが Microsoft SQL Server 2005 Analysis Services (SSAS) のインスタンスに接続されている場合、は `CONNID` サーバープロセス識別子 (SPID) にマップされます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
