---
title: CreateDebuggingInterfaceFromVersion 関数
ms.date: 03/30/2017
api_name:
- CreateDebuggingInterfaceFromVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function [.NET Framework hosting]
ms.assetid: a746a849-463c-44f5-a2f0-9e812ed8bcc3
topic_type:
- apiref
ms.openlocfilehash: 6f5eec282aec6a2757664023ce8031410e316f10
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501847"
---
# <a name="createdebugginginterfacefromversion-function"></a>CreateDebuggingInterfaceFromVersion 関数
指定されたバージョン情報に基づいて[ICorDebug](../debugging/icordebug-interface.md)オブジェクトを作成します。  
  
 この関数は、.NET Framework 4 では廃止されています。 代わりに、共通言語ランタイム (CLR) 2.0 のインターフェイスを取得するには、 [ICLRRuntimeInfo:: GetInterface](iclrruntimeinfo-getinterface-method.md)メソッドを使用して、クラス識別子 CLSID_CLRDebuggingLegacy とインターフェイス識別子 IID_ICorDebug を指定します。 CLR 4 以降のインターフェイスを取得するには、 [Clrcreateinstance](clrcreateinstance-function.md)関数を呼び出し、クラス識別子 CLSID_CLRDebugging とインターフェイス識別子 IID_ICLRDebugging を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  int      iDebuggerVersion,
    [in]  LPCWSTR  szDebuggeeVersion,
    [out] IUnknown **ppCordb  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `iDebuggerVersion`  
 から`ICorDebug`デバッガーによって想定されているのバージョン。 有効な値については、 [Cordebuginterfaceversion](../debugging/cordebuginterfaceversion-enumeration.md)列挙体を参照してください。  
  
 `szDebuggeeVersion`  
 からデバッグ対象のアプリケーションまたはプロセスに関連付けられている共通言語ランタイムのバージョン。 この値を取得する方法については、「 [Getversionfromprocess](getversionfromprocess-function.md) 」または「 [Getversionfromprocess](getrequestedruntimeversion-function.md)メソッド」を参照してください。  
  
 `ppCordb`  
 入出力オブジェクトへのポインターを受け取る位置 `ICorDebug` 。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の値に加えて、Winerror.h ファイルで定義されている標準 COM エラーコードを返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_INVALIDARG|`szDebuggeeVersion`または `ppCordb` が null であるか、またはバージョン文字列が正しくありません。|  
  
## <a name="remarks"></a>解説  
 パラメーターは、 `szDebuggeeVersion` 対応するバージョンの mscordbi.dll にマップされます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
