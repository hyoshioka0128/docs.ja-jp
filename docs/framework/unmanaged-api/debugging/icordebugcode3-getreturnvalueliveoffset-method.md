---
title: ICorDebugCode3::GetReturnValueLiveOffset メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugCode3.GetReturnValueLiveOffset
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode3::GetReturnValueLiveOffset
helpviewer_keywords:
- ICorDebugCode3::GetReturnValueLiveOffset method [.NET Framework debugging]
- GetReturnValueLiveOffset method [.NET Framework debugging]
ms.assetid: 8c2ff5d8-8c04-4423-b1e1-e1c8764b36d3
topic_type:
- apiref
ms.openlocfilehash: 2cb4c79601061ab8473d6d7ca50c4ed2f92b01c4
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893434"
---
# <a name="icordebugcode3getreturnvalueliveoffset-method"></a>ICorDebugCode3::GetReturnValueLiveOffset メソッド
指定した IL オフセットについて、デバッガーが関数からの戻り値を取得できるように、ブレークポイントを配置する必要があるネイティブなオフセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetReturnValueLiveOffset(  
    [in] ULONG32 ILoffset,  
    [in] ULONG32 bufferSize,
    [out] ULONG32 *pFetched,
    [out, size_is(buffersize), length_is(*pFetched)] ULong32 pOffsets[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ILoffset`  
 オフセット IL。 関数呼び出しサイトであることが必要です。そうでない場合、関数呼び出しは失敗します。  
  
 `bufferSize`  
 `pOffsets` を格納できるバイト数。  
  
 `pFetched`  
 実際に返されたオフセットの数へのポインター。 通常、この値は 1 ですが、単一の IL 命令が複数の `CALL` アセンブリ命令にマップする場合があります。  
  
 `pOffsets`  
 ネイティブ オフセットの配列。 通常、`pOffsets` には単一のオフセットが含まれますが、単一の IL 命令が複数の `CALL` アセンブリ命令に対する複数のマップに対応する場合があります。  
  
## <a name="remarks"></a>解説  
 このメソッドは、参照型を返すメソッドの戻り値を取得するために、 [ICorDebugILFrame3:: GetReturnValueForILOffset](icordebugilframe3-getreturnvalueforiloffset-method.md)メソッドと共に使用されます。 関数呼び出しサイトに対する IL オフセットをこのメソッドに渡すと、1 つ以上のネイティブ オフセットが返されます。 これによってデバッガーは、関数内のこうしたネイティブ オフセット上でブレークポイントを設定できます。 デバッガーがいずれかのブレークポイントにヒットすると、このメソッドに渡された同じ IL オフセットを[ICorDebugILFrame3:: GetReturnValueForILOffset](icordebugilframe3-getreturnvalueforiloffset-method.md)メソッドに渡して、戻り値を取得できます。 この場合、デバッガーは設定したブレークポイントすべてをクリアする必要があります。  
  
> [!WARNING]
> および`ICorDebugCode3::GetReturnValueLiveOffset` [ICorDebugILFrame3:: GetReturnValueForILOffset](icordebugilframe3-getreturnvalueforiloffset-method.md)メソッドを使用すると、参照型の戻り値の情報のみを取得できます。 値型 (つまり、<xref:System.ValueType> から派生するすべての型) からの戻り値情報の取得はサポートされません。  
  
 この関数は、次の表に示す `HRESULT` 値を返します。  
  
|`HRESULT` 値|説明|  
|---------------------|-----------------|  
|`S_OK`|成功しました。|  
|`CORDBG_E_INVALID_OPCODE`|指定した IL オフセット サイトが呼び出し命令ではないか、関数が `void` を返しています。|  
|`CORDBG_E_UNSUPPORTED`|指定した IL オフセットは適切な呼び出しですが、取得する戻り値の型がサポートされていません。|  
  
 `ICorDebugCode3::GetReturnValueLiveOffset` メソッドは、x86 ベースおよび AMD64 システムでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetReturnValueForILOffset メソッド](icordebugilframe3-getreturnvalueforiloffset-method.md)
- [ICorDebugCode3 インターフェイス](icordebugcode3-interface.md)
