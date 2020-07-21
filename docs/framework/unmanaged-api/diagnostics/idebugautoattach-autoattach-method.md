---
title: IDebugAutoAttach::AutoAttach メソッド
ms.date: 03/30/2017
api_name:
- IDebugAutoAttach.AutoAttach
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- IDebugAutoAttach::AutoAttach
helpviewer_keywords:
- AutoAttach method [.NET Framework debugging]
- IDebugAutoAttach::AutoAttach method [.NET Framework debugging]
ms.assetid: 3cf3bd9c-7d88-4afa-a476-94cdc7609aa6
topic_type:
- apiref
ms.openlocfilehash: aae03b0dc76639c50f4615d41eef73990226b5f7
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442125"
---
# <a name="idebugautoattachautoattach-method"></a>IDebugAutoAttach::AutoAttach メソッド
サーバーによって呼び出されたデバッガーの自動アタッチを実行します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AutoAttach  
(  
    [in]  REFGUID   guidPort,  
    [in]  DWORD     dwPid,  
    [in]  AUTOATTACH_PROGRAM_TYPE dwProgramType,  
    [in]  DWORD     dwProgramId,  
    [in]  LPCWSTR   pszSessionId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `guidPort`  
 から常にに設定 `GUID_NULL` します。  
  
 `dwPid`  
 からプロセス ID。通常は関数を使用して取得さ `GetCurrentProcessId` れます。  
  
 `dwProgramType`  
 からプログラムの種類: `AUTOATTACH_PROGRAM_WIN32` 、 `AUTOATTACH_PROGRAM_COMPLUS` 、または `AUTOATTACH_PROGRAM_UNKNOWN` 。  
  
 `dwProgramId`  
 からプログラム ID。  
  
 `pszSessionId`  
 からデバッグ動詞によって渡された文字列。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** DbgAutoAttach .h  
  
## <a name="see-also"></a>関連項目

- [IDebugAutoAttach インターフェイス](idebugautoattach-interface.md)
