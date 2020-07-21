---
title: ICorDebugModule2::ApplyChanges メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ApplyChanges
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ApplyChanges
helpviewer_keywords:
- ApplyChanges method [.NET Framework debugging]
- ICorDebugModule2::ApplyChanges method [.NET Framework debugging]
ms.assetid: 96fa3406-6a6f-41a1-88c6-d9bc5d1a16d1
topic_type:
- apiref
ms.openlocfilehash: 99824e9a7fd759fb30bfa377156fc28eb934a2b4
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212218"
---
# <a name="icordebugmodule2applychanges-method"></a>ICorDebugModule2::ApplyChanges メソッド
メタデータの変更と、Microsoft 中間言語 (MSIL) コードの変更を実行中のプロセスに適用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ApplyChanges (  
    [in] ULONG                       cbMetadata,  
    [in, size_is(cbMetadata)] BYTE   pbMetadata[],  
    [in] ULONG                       cbIL,  
    [in, size_is(cbIL)] BYTE         pbIL[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cbMetadata`  
 からデルタメタデータのサイズ (バイト単位)。  
  
 `pbMetadata`  
 からデルタメタデータを格納しているバッファー。 バッファーのアドレスは、 [IMetaDataEmit2:: SaveDeltaToMemory](../metadata/imetadataemit2-savedeltatomemory-method.md)メソッドから返されます。  
  
 メタデータ内の相対仮想アドレス (RVAs) は、MSIL コードの先頭に対して相対的に指定する必要があります。  
  
 `cbIL`  
 からデルタ MSIL コードのサイズ (バイト単位)。  
  
 `pbIL`  
 から更新された MSIL コードを格納しているバッファー。  
  
## <a name="remarks"></a>Remarks  
 パラメーターは、 `pbMetadata` ( [IMetaDataEmit2:: SaveDeltaToMemory](../metadata/imetadataemit2-savedeltatomemory-method.md)によって出力される) 特別なデルタメタデータ形式です。 `pbMetadata`以前のメタデータをベースとして受け取り、そのベースに適用する個々の変更について説明します。  
  
 これに対し、のパラメーターには、 `pbIL[` 更新されたメソッドの新しい msil が含まれています。これは、そのメソッドの前の msil を完全に置き換えることを目的としています。  
  
 デルタ MSIL とメタデータがデバッガーのメモリ内に作成されると、デバッガーはを呼び出して、 `ApplyChanges` 変更を共通言語ランタイム (CLR) に送信します。 ランタイムはそのメタデータテーブルを更新し、新しい MSIL をプロセスに配置して、新しい MSIL の just-in-time (JIT) コンパイルを設定します。 変更が適用されると、デバッガーは[IMetaDataEmit2:: ResetENCLog](../metadata/imetadataemit2-resetenclog-method.md)を呼び出して、次の編集セッションの準備を行う必要があります。 デバッガーはプロセスを続行できます。  
  
 デバッガーは、 `ApplyChanges` デルタメタデータを持つモジュールでを呼び出すたびに、変更を出力するために使用されるコピーを除き、そのモジュールのメタデータのすべてのコピーで同じデルタメタデータを使用して[IMetaDataEmit:: ApplyEditAndContinue](../metadata/imetadataemit-applyeditandcontinue-method.md)を呼び出す必要があります。 メタデータのコピーが実際のメタデータと同期しなくなる場合、デバッガーは常にそのコピーを破棄して新しいコピーを取得できます。  
  
 メソッドが失敗した場合 `ApplyChanges` 、デバッグセッションは無効な状態にあり、再起動する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
