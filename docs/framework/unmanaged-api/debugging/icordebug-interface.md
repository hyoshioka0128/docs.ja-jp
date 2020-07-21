---
title: ICorDebug インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebug
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug
helpviewer_keywords:
- ICorDebug interface [.NET Framework debugging]
ms.assetid: 33f431d7-ab1a-494d-8af2-20ab15aba194
topic_type:
- apiref
ms.openlocfilehash: 66b50bad0e8d2622922da96c213643ac3be83a9e
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895371"
---
# <a name="icordebug-interface"></a>ICorDebug インターフェイス
開発者が共通言語ランタイム (CLR) 環境でアプリケーションをデバッグできるようにするメソッドを提供します。  
  
> [!NOTE]
> 混合モード (マネージコードとネイティブコード) のデバッグは、Windows 95、Windows 98、または Windows ME ではサポートされておらず、x86 以外のプラットフォーム (IA64 や AMD64 など) ではサポートされていません。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CanLaunchOrAttach メソッド](icordebug-canlaunchorattach-method.md)|現在のコンピューターおよびランタイム構成のコンテキスト内で、新しいプロセスを起動するか、指定したプロセスにアタッチするかを決定します。|  
|[CreateProcess メソッド](icordebug-createprocess-method.md)|デバッガーの制御下でプロセスとそのプライマリスレッドを起動します。|  
|[DebugActiveProcess メソッド](icordebug-debugactiveprocess-method.md)|デバッガーを既存のプロセスにアタッチします。|  
|[EnumerateProcesses メソッド](icordebug-enumerateprocesses-method.md)|デバッグ中のプロセスの列挙子を取得します。|  
|[GetProcess メソッド](icordebug-getprocess-method.md)|指定されたプロセス ID を持つ "いいプロセス" オブジェクトを返します。|  
|[Initialize メソッド](icordebug-initialize-method.md)|`ICorDebug` オブジェクトを初期化します。|  
|[SetManagedHandler メソッド](icordebug-setmanagedhandler-method.md)|マネージイベントのイベントハンドラーオブジェクトを指定します。|  
|[SetUnmanagedHandler メソッド](icordebug-setunmanagedhandler-method.md)|アンマネージイベントのイベントハンドラーオブジェクトを指定します。|  
|[Terminate メソッド](icordebug-terminate-method.md)|オブジェクトを`ICorDebug`終了します。|  
  
## <a name="remarks"></a>解説  
 `ICorDebug`デバッガープロセスのイベント処理ループを表します。 デバッガーは、このインターフェイスを解放する前に、デバッグされているすべてのプロセスからの "ExitProcess" コール[バック](icordebugmanagedcallback-exitprocess-method.md)を待機する必要があります。  
  
 `ICorDebug`オブジェクトは、さらに管理されているすべてのデバッグを制御するための初期オブジェクトです。 .NET Framework バージョン1.0 および1.1 では、このオブジェクトは COM `CoClass`から作成されたオブジェクトでした。 .NET Framework バージョン2.0 では、このオブジェクトは`CoClass`オブジェクトではなくなりました。 これは、バージョンを認識する[CreateDebuggingInterfaceFromVersion](../hosting/createdebugginginterfacefromversion-function.md)関数によって作成される必要があります。 この新しい作成関数を使用すると、クライアントは特定`ICorDebug`のバージョンのデバッグ API もエミュレートするの特定の実装を取得できます。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
