---
title: ICLRDebugging::OpenVirtualProcess メソッド
ms.date: 03/30/2017
api_name:
- ICLRDebugging.OpenVirtualProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebugging::OpenVirtualProcess
helpviewer_keywords:
- OpenVirtualProcess method [.NET Framework debugging]
- ICLRDebugging::OpenVirtualProcess method [.NET Framework debugging]
ms.assetid: e8ab7c41-d508-4ed9-8a31-ead072b5a314
topic_type:
- apiref
ms.openlocfilehash: 1598130eb097655d3e83689956eb3614103eb573
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860367"
---
# <a name="iclrdebuggingopenvirtualprocess-method"></a>ICLRDebugging::OpenVirtualProcess メソッド
プロセスに読み込まれた共通言語ランタイム (CLR) モジュールに対応する、コンポーネントインターフェイスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OpenVirtualProcess(  
    [in] ULONG64 moduleBaseAddress,  
    [in] IUnknown * pDataTarget,  
    [in] ICLRDebuggingLibraryProvider * pLibraryProvider,  
    [in] CLR_DEBUGGING_VERSION * pMaxDebuggerSupportedVersion,  
    [in] REFIID riidProcess,  
    [out, iid_is(riidProcess)] IUnknown ** ppProcess,  
    [in, out] CLR_DEBUGGING_VERSION * pVersion,  
    [out] CLR_DEBUGGING_PROCESS_FLAGS * pdwFlags);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleBaseAddress`  
 からターゲットプロセス内のモジュールのベースアドレス。 指定したモジュールが CLR モジュールでない場合、COR_E_NOT_CLR が返されます。  
  
 `pDataTarget`  
 からマネージデバッガーがプロセスの状態を検査できるデータターゲットの抽象化。 デバッガーでは、、のように、によっては、[このインターフェイスを](icordebugdatatarget-interface.md)実装してください。 デバッグ対象の CLR がコンピューターにローカルにインストールされていないシナリオをサポートするには、 [ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md)インターフェイスを実装する必要があります。  
  
 `pLibraryProvider`  
 からライブラリプロバイダーのコールバックインターフェイス。バージョン固有のデバッグライブラリをオンデマンドで検索し、読み込むことができます。 このパラメーターは、または`ppProcess` `pFlags`がでは`null`ない場合にのみ必要です。  
  
 `pMaxDebuggerSupportedVersion`  
 からこのデバッガーがデバッグできる CLR の最大バージョン。 このデバッガーでサポートされている最新の CLR バージョンからメジャー、マイナー、ビルドの各バージョンを指定し、将来の CLR サービスリリースに対応するためにリビジョン番号を65535に設定する必要があります。  
  
 `riidProcess`  
 から取得するコード処理インターフェイスの ID。 現時点で許容される値は、IID_CORDEBUGPROCESS3、IID_CORDEBUGPROCESS2、および IID_CORDEBUGPROCESS だけです。  
  
 `ppProcess`  
 入出力によって`riidProcess`識別される COM インターフェイスへのポインター。  
  
 `pVersion`  
 [入力、出力]CLR のバージョン。 入力時には、この値`null`をにすることができます。 また、 [CLR_DEBUGGING_VERSION](clr-debugging-version-structure.md)構造体を指すこともできます。この場合、 `wStructVersion`構造体のフィールドを 0 (ゼロ) に初期化する必要があります。  
  
 出力時には、 `CLR_DEBUGGING_VERSION`返された構造体に CLR のバージョン情報が格納されます。  
  
 `pdwFlags`  
 入出力指定されたランタイムに関する情報フラグ。 フラグの説明については、 [CLR_DEBUGGING_PROCESS_FLAGS](clr-debugging-process-flags-enumeration.md)のトピックを参照してください。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pDataTarget` は `null` です。|  
|CORDBG_E_LIBRARY_PROVIDER_ERROR|[ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md)コールバックによってエラーが返されたか、有効なハンドルが提供されていません。|  
|CORDBG_E_MISSING_DATA_TARGET_INTERFACE|`pDataTarget`は、このバージョンのランタイムに必要なデータターゲットインターフェイスを実装していません。|  
|CORDBG_E_NOT_CLR|指定されたモジュールは CLR モジュールではありません。 この HRESULT は、メモリが破損している、モジュールが使用できない、または CLR バージョンが shim バージョンより後であるために CLR モジュールが検出できない場合にも返されます。|  
|CORDBG_E_UNSUPPORTED_DEBUGGING_MODEL|このランタイムバージョンでは、このデバッグモデルはサポートされていません。 現時点では、.NET Framework 4 より前のバージョンの CLR では、デバッグモデルはサポートされていません。 この`pwszVersion`エラーが発生すると、出力パラメーターは正しい値に設定されたままになります。|  
|CORDBG_E_UNSUPPORTED_FORWARD_COMPAT|CLR のバージョンが、このデバッガーがサポートするために要求するバージョンよりも大きくなっています。 この`pwszVersion`エラーが発生すると、出力パラメーターは正しい値に設定されたままになります。|  
|E_NO_INTERFACE|`riidProcess`インターフェイスは使用できません。|  
|CORDBG_E_UNSUPPORTED_VERSION_STRUCT|構造`CLR_DEBUGGING_VERSION`体に、の`wStructVersion`認識された値がありません。 現時点で許容される値は0のみです。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
