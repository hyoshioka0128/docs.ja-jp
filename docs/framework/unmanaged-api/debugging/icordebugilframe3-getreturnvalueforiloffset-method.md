---
title: ICorDebugILFrame3::GetReturnValueForILOffset メソッド
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
api_name:
- ICorDebugILFrame3.GetReturnValueForILOffset
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 06522727-5f64-4391-9331-11386883c352
topic_type:
- apiref
ms.openlocfilehash: f6a54ab9efa7ca97bcdb64afcde8812f2b5e44e9
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210073"
---
# <a name="icordebugilframe3getreturnvalueforiloffset-method"></a>ICorDebugILFrame3::GetReturnValueForILOffset メソッド
関数の戻り値をカプセル化する "ICorDebugValue" オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetReturnValueForILOffset(  
    ULONG32 ILoffset,
    [out] ICorDebugValue **ppReturnValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ILOffset`  
 オフセット IL。 「解説」を参照してください。  
  
 `ppReturnValue`  
 関数呼び出しの戻り値に関する情報を提供する "ICorDebugValue" インターフェイスオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、メソッドの戻り値を取得するために、 [ICorDebugCode3:: Getreturnvalu Veoffset](icordebugcode3-getreturnvalueliveoffset-method.md)メソッドと共に使用されます。 次の 2 つのコード例で示すように、これは戻り値が無視されるメソッドの場合に特に役立ちます。 1 番目の例では、<xref:System.Int32.TryParse%2A?displayProperty=nameWithType> メソッドを呼び出しますが、メソッドの戻り値を無視します。  
  
 [!code-csharp[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv1.cs#1)]
 [!code-vb[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv1.vb#1)]  
  
 2 番目の例は、より一般的なデバッグの問題を示しています。 メソッド呼び出しで引数としてメソッドが使用されるため、デバッガーで呼び出されたメソッドをステップ実行する場合に限り、戻り値にアクセスできます。 多くの場合、特に呼び出されたメソッドが外部ライブラリで定義されている場合にはアクセスできません。  
  
 [!code-csharp[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv2.cs#2)]
 [!code-vb[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv2.vb#2)]  
  
 [ICorDebugCode3:: Getreturnvalu veoffset](icordebugcode3-getreturnvalueliveoffset-method.md)メソッドに関数呼び出しサイトへの IL オフセットを渡すと、1つ以上のネイティブオフセットが返されます。 これによってデバッガーは、関数内のこうしたネイティブ オフセット上でブレークポイントを設定できます。 デバッガーがいずれかのブレークポイントに到達すると、戻り値を取得するためにこのメソッドに同じ IL オフセットを渡すことができます。 この場合、デバッガーは設定したブレークポイントすべてをクリアする必要があります。  
  
> [!WARNING]
> [ICorDebugCode3:: Getreturnvalu Veoffset メソッド](icordebugcode3-getreturnvalueliveoffset-method.md)とメソッドを使用すると、 `ICorDebugILFrame3::GetReturnValueForILOffset` 参照型の戻り値の情報のみを取得できます。 値型 (つまり、<xref:System.ValueType> から派生するすべての型) からの戻り値情報の取得はサポートされません。  
  
 パラメーターで指定された IL オフセットは `ILOffset` 関数呼び出しサイトに存在する必要があります。また、同じ il オフセットの[ICorDebugCode3:: Getreturnvalu veoffset](icordebugcode3-getreturnvalueliveoffset-method.md)メソッドによって返されるネイティブオフセットに設定されているブレークポイントで、デバッグ対象を停止する必要があります。 デバッグ対象が指定の IL オフセットに対して正確な場所で停止しない場合、API は失敗します。  
  
 関数呼び出しで値が返されない場合、API は失敗します。  
  
 `ICorDebugILFrame3::GetReturnValueForILOffset` メソッドは、x86 ベースおよび AMD64 システムでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetReturnValueLiveOffset メソッド](icordebugcode3-getreturnvalueliveoffset-method.md)
- [ICorDebugILFrame3 インターフェイス](icordebugilframe3-interface.md)
