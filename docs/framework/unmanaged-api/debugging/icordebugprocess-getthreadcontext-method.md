---
title: ICorDebugProcess::GetThreadContext メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetThreadContext
helpviewer_keywords:
- ICorDebugProcess::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: 5b132ef1-8d4b-4525-89b3-54123596c194
topic_type:
- apiref
ms.openlocfilehash: 2bdbf373144e2fb49074cfd035e7b0ffe3c8c291
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212890"
---
# <a name="icordebugprocessgetthreadcontext-method"></a>ICorDebugProcess::GetThreadContext メソッド
このプロセス内の指定されたスレッドのコンテキストを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetThreadContext(  
    [in] DWORD threadID,  
    [in] ULONG32 contextSize,  
    [in, out, length_is(contextSize), size_is(contextSize)]  
    BYTE context[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `threadID`  
 からコンテキストを取得するスレッドの ID。  
  
 `contextSize`  
 [in] `context` 配列のサイズ。  
  
 `context`  
 [入力、出力]スレッドのコンテキストを記述するバイト配列。  
  
 コンテキストは、スレッドが実行されているプロセッサのアーキテクチャを指定します。  
  
## <a name="remarks"></a>Remarks  
 デバッガーは、Win32 メソッドではなく、このメソッドを呼び出す必要があります。これは、 `GetThreadContext` スレッドが実際には "ハイジャック" 状態にあり、そのコンテキストが一時的に変更されている可能性があるためです。 このメソッドは、スレッドがネイティブコード内にある場合にのみ使用してください。 マネージコード内のスレッドには、コード[を使用し](icordebugregisterset-interface.md)ます。  
  
 返されるデータは、現在のプラットフォームのコンテキスト構造です。 Win32 メソッドの場合と同様に、 `GetThreadContext` 呼び出し元は、 `context` このメソッドを呼び出す前にパラメーターを初期化する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
