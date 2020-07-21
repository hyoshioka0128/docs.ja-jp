---
title: ICorDebugChain::EnumerateFrames メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugChain.EnumerateFrames
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::EnumerateFrames method
helpviewer_keywords:
- EnumerateFrames method [.NET Framework debugging]
- ICorDebugChain::EnumerateFrames method [.NET Framework debugging]
ms.assetid: 9fcefa98-750d-4168-8915-8173a43accf2
topic_type:
- apiref
ms.openlocfilehash: c8a62d8b4a4db0f36d991c32dbfc5bad68780f1b
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894691"
---
# <a name="icordebugchainenumerateframes-method"></a>ICorDebugChain::EnumerateFrames メソッド
チェーン内のすべてのマネージスタックフレームが格納された列挙子を取得します。これは、最新のフレームから始まります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateFrames (  
    [out] ICorDebugFrameEnum **ppFrames  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppFrames`  
 入出力スタックフレームの列挙子である、テキストフレームの列挙型オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 チェーンは、スレッドの物理呼び出し履歴を表します。  
  
 メソッド`EnumerateFrames`は、マネージドチェーンに対してのみ呼び出す必要があります。 デバッグ API には、アンマネージチェーンに含まれるフレームを取得するためのメソッドが用意されていません。 デバッガーは、この情報を取得するために他の手段を使用する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
