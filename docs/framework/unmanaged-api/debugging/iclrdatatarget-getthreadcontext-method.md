---
title: ICLRDataTarget::GetThreadContext メソッド
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetThreadContext
helpviewer_keywords:
- ICLRDataTarget::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
ms.assetid: b9d8c3b5-3a2e-4225-95d4-dd052c4532c3
topic_type:
- apiref
ms.openlocfilehash: 5c0fb023dd355f3a9c1ed846913f86b354592ed5
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860611"
---
# <a name="iclrdatatargetgetthreadcontext-method"></a>ICLRDataTarget::GetThreadContext メソッド
ターゲットプロセス内の指定されたスレッドの現在の実行コンテキストを取得します。 このメソッドは、共通言語ランタイムのデータアクセスサービスによって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextFlags,  
    [in] ULONG32            contextSize,  
    [out, size_is(contextSize)]
        BYTE                *context  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `threadID`  
 からターゲットプロセス内のスレッドのオペレーティングシステム識別子。  
  
 `contextFlags`  
 からコンテキストのどの部分を返すかを指定するフラグ。 実装は、少なくともこれらのコンテキストの部分を返します。  
  
 `contextSize`  
 からコンテキストのサイズ。  
  
 `context`  
 入出力コンテキストを配置するバッファーへのポインター。  
  
 `context`バッファー内のデータは、Win32 `CONTEXT`構造体の形式である必要があります。 コンテキストはプロセッサ固有のレジスタデータを指定するため、Win32 `CONTEXT`構造体の定義はプロセッサのアーキテクチャによって異なります。 Win32 `CONTEXT`構造体の定義については、winnt.h ヘッダーファイルを参照してください。  
  
## <a name="remarks"></a>解説  
 このメソッドは、デバッグ アプリケーションの作成者によって実装されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataTarget インターフェイス](iclrdatatarget-interface.md)
