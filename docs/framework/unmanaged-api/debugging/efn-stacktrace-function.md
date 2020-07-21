---
title: _EFN_StackTrace 関数
ms.date: 03/30/2017
api_name:
- _EFN_StackTrace
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_StackTrace
helpviewer_keywords:
- _EFN_StackTrace function [.NET Framework debugging]
ms.assetid: caea7754-867c-4360-a65c-5ced4408fd9d
topic_type:
- apiref
ms.openlocfilehash: a725aa2c0f1fdea523bbf7cba880bc805f855782
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860738"
---
# <a name="_efn_stacktrace-function"></a>\_EFN\_StackTrace 関数
マネージド スタック トレースのテキスト表現および `CONTEXT` レコードの配列 (アンマネージド コードとマネージド コードの間の各移行につき 1 つ) を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CALLBACK _EFN_StackTrace(  
    [in]  PDEBUG_CLIENT  Client,  
    [out] WCHAR          wszTextOut[],  
    [out] size_t         *puiTextLength,  
    [out] LPVOID         pTransitionContexts,  
    [out] size_t         *puiTransitionContextCount,  
    [in]  size_t         uiSizeOfContext,  
    [in]  DWORD          Flags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `Client`  
 からデバッグ中のクライアント。  
  
 `wszTextOut`  
 入出力スタックトレースのテキスト表現。  
  
 `puiTextLength`  
 入出力内`wszTextOut`の文字数へのポインター。  
  
 `pTransitionContexts`  
 入出力遷移コンテキストの配列。  
  
 `puiTransitionContextCount`  
 入出力配列内の遷移コンテキストの数へのポインター。  
  
 `uiSizeOfContext`  
 からコンテキスト構造のサイズ。  
  
 `Flags`  
 からを0または SOS_STACKTRACE_SHOWADDRESSES (0x01) のいずれかに設定すると、EBP レジスタと、各`module!functionname`行の前に入力スタックポインター (ESP) が表示されます。  
  
## <a name="remarks"></a>解説  
 この`_EFN_StackTrace`構造体は、WinDbg プログラムインターフェイスから呼び出すことができます。 パラメーターは次のように使用されます。  
  
- が`wszTextOut` null で、 `puiTextLength`が null でない場合、関数はの`puiTextLength`文字列長を返します。  
  
- が`wszTextOut` null でない場合、関数はによっ`wszTextOut`て`puiTextLength`示される場所までテキストを格納します。 バッファーに十分な空き領域がある場合は、正常に返されます。バッファーの長さが十分でない場合は E_OUTOFMEMORY を返します。  
  
- とが両方と`pTransitionContexts` `puiTransitionContextCount`も null の場合、関数の移行部分は無視されます。 この場合、関数は呼び出し元に関数名のみのテキスト出力を提供します。  
  
- が`pTransitionContexts` null で、 `puiTransitionContextCount`が null でない場合、関数はで`puiTransitionContextCount`必要なコンテキストエントリの数を返します。  
  
- が`pTransitionContexts` null でない場合、関数はそれを長さ`puiTransitionContextCount`の構造体の配列として扱います。 構造体のサイズはに`uiSizeOfContext`よって指定され、 [simplecontext](stacktrace-simplecontext-structure.md)または`CONTEXT`アーキテクチャのサイズである必要があります。  
  
- `wszTextOut`は、次の形式で記述されます。  
  
    ```output  
    "<ModuleName>!<Function Name>[+<offset in hex>]  
    ...  
    (TRANSITION)  
    ..."  
    ```  
  
- 16進数のオフセットが0x0 の場合、オフセットは書き込まれません。  
  
- 現在コンテキスト内にあるスレッドにマネージコードがない場合、関数は SOS_E_NOMANAGEDCODE を返します。  
  
- パラメーター `Flags`は、各`module!functionname`行の前に EBP と ESP を表示する場合は0または SOS_STACKTRACE_SHOWADDRESSES になります。 既定値は0です。  
  
    ```cpp  
    #define SOS_STACKTRACE_SHOWADDRESSES   0x00000001  
    ```  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** SOS_Stacktrace  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ グローバル静的関数](debugging-global-static-functions.md)
