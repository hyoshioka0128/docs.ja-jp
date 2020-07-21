---
title: ICorDebugSymbolProvider::GetMethodLocalSymbols メソッド
ms.date: 03/30/2017
ms.assetid: 8b989e38-e779-49d1-9e90-f1f920484b08
ms.openlocfilehash: 7e9aa01a3fa1c90b0ab4f85970c4eb294b9a4904
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379613"
---
# <a name="icordebugsymbolprovidergetmethodlocalsymbols-method"></a>ICorDebugSymbolProvider::GetMethodLocalSymbols メソッド
メソッドの指定の相対仮想アドレス (RVA) で、そのメソッドのローカル シンボルを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMethodLocalSymbols(  
   [in] ULONG32 nativeRVA,  
   [in] ULONG32 cRequestedSymbols,  
   [out] ULONG32 *pcFetchedSymbols,  
   [out, size_is(cRequestedSymbols), length_is(*pcFetchedSymbols)] ICorDebugVariableSymbol *pSymbols[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `nativeRVA`  
 [in] メソッドのネイティブ相対仮想アドレス。  
  
 `cRequestedSymbols`  
 [in] ローカル シンボルの要求数。  
  
 `pcFetchedSymbols`  
 [out] メソッドによって取得されたシンボル数へのポインター。  
  
 `pcFetchedSymbols`  
 入出力メソッドのローカルシンボルを格納している[ICorDebugVariableSymbol](icordebugvariablesymbol-interface.md)配列へのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetMethodParameterSymbols メソッド](icordebugsymbolprovider-getmethodparametersymbols-method.md)
- [ICorDebugSymbolProvider インターフェイス](icordebugsymbolprovider-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
