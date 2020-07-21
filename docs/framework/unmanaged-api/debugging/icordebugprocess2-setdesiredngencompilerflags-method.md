---
title: ICorDebugProcess2::SetDesiredNGENCompilerFlags メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetDesiredNGENCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags
helpviewer_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags method [.NET Framework debugging]
- SetDesiredNGENCompilerFlags method [.NET Framework debugging]
ms.assetid: 98320175-7c5e-4dbb-8683-86fa82e2641f
topic_type:
- apiref
ms.openlocfilehash: 366a48e5f6abd92f0c6f796f40bdd263181da4a8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213479"
---
# <a name="icordebugprocess2setdesiredngencompilerflags-method"></a>ICorDebugProcess2::SetDesiredNGENCompilerFlags メソッド
ランタイムがそのイメージを現在のプロセスに読み込むために、プリコンパイル済みイメージに埋め込む必要があるフラグを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetDesiredNGENCompilerFlags (  
    [in] DWORD    pdwFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pdwFlags`  
 から適切なプリコンパイル済みイメージを選択するために使用されるコンパイラフラグを指定する[CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>Remarks  
 メソッドは、 `SetDesiredNGENCompilerFlags` プリコンパイル済みイメージに埋め込まれる必要があるフラグを指定します。これにより、ランタイムはそのイメージをこのプロセスに読み込みます。 このメソッドによって設定されるフラグは、正しいプリコンパイル済みイメージを選択するためにのみ使用されます。 そのようなイメージが存在しない場合、ランタイムは Microsoft 中間言語 (MSIL) イメージと just-in-time (JIT) コンパイラを読み込みます。 その場合でも、デバッガーは[ICorDebugModule2:: SetJITCompilerFlags](icordebugmodule2-setjitcompilerflags-method.md)メソッドを使用して、JIT コンパイルに必要なフラグを設定する必要があります。  
  
 イメージが読み込まれるときに、そのイメージに対して一部の JIT コンパイルを実行する必要がある場合 (イメージにジェネリックが含まれている場合)、メソッドによって指定されたコンパイラフラグ `SetDesiredNGENCompilerFlags` が追加の jit コンパイルに適用されます。  
  
 このメソッドは、の `SetDesiredNGENCompilerFlags` メソッドを[ICorDebugManagedCallback::CreateProcess](icordebugmanagedcallback-createprocess-method.md)呼び出さなければなりません。 その後、メソッドを呼び出そうとすると `SetDesiredNGENCompilerFlags` 失敗します。 また、列挙型で定義されていないフラグや、指定されたプロセスに対して有効ではないフラグを設定しようとすると `CorDebugJITCompilerFlags` 失敗します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebug インターフェイス](icordebug-interface.md)
- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
