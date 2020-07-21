---
title: ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3.GetCachedWinRTTypesForIIDs
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs
helpviewer_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs method, [.NET Framework debugging]
- GetCachedWinRTTypesForIIDs method, ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 23682ca0-1bcf-48e6-996e-69f7ba337682
topic_type:
- apiref
ms.openlocfilehash: f8e92ec4f813e8810273a1514298d0739a3d2406
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179055"
---
# <a name="icordebugappdomain3getcachedwinrttypesforiids-method"></a>ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs メソッド
インターフェイス識別子に基づいて、アプリケーション ドメインにキャッシュされた Windows ランタイム型の列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCachedWinRTTypesForIIDs (
    [in]  ULONG32            cReqTypes,  
    [in]  GUID                *iidsToResolve,  
    [out] ICorDebugTypeEnum   **ppTypesEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cReqTypes`  
 [in]必要な型の数。  
  
 `iidsToResolve`  
 [in]取得する Windows ランタイム型のマネージ表現に対応するインターフェイス識別子を含む配列へのポインター。  
  
 `ppTypesEnum`  
 [アウト]で取得した Windows ランタイム型のキャッシュされたマネージ表現の列挙を可能にする "ICorDebugTypeEnum" インターフェイス オブジェクトのアドレスへのポインター `iidsToResolve`。  
  
## <a name="remarks"></a>解説  
 メソッドが特定のインターフェイス識別子の情報を取得できない場合、"ICorDebugTypeEnum" コレクション内の対応するエントリは、データ取得`ELEMENT_TYPE_END`の問題または`ELEMENT_TYPE_VOID`不明なインターフェイス識別子のエラーの種類を持ちます。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** ウィンドウズランタイム  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugAppDomain3 インターフェイス](icordebugappdomain3-interface.md)
