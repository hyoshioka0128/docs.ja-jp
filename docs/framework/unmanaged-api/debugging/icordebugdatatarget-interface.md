---
title: ICorDebugDataTarget インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget
helpviewer_keywords:
- ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: df5f05be-bed7-4f3c-bc89-dbb435d79a0b
topic_type:
- apiref
ms.openlocfilehash: 54272dd18a12715bab58ec1b1a4c1dc00e4bf12b
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976526"
---
# <a name="icordebugdatatarget-interface"></a>ICorDebugDataTarget インターフェイス
特定のターゲット プロセスにアクセスするためのコールバック インターフェイスが用意されています。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetPlatform メソッド](icordebugdatatarget-getplatform-method.md)|ターゲットプロセスが実行されているプラットフォーム (プロセッサアーキテクチャやオペレーティングシステムなど) に関する情報を提供します。|  
|[ReadVirtual メソッド](icordebugdatatarget-readvirtual-method.md)|指定したアドレスを開始位置として連続したメモリのブロックを取得し、指定したバッファー内でそれを返します。|  
|[GetThreadContext メソッド](icordebugdatatarget-getthreadcontext-method.md)|指定されたスレッドの現在のスレッドコンテキストを要求します。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugDataTarget`およびそのメソッドの特性は次のとおりです。  
  
- デバッグサービスは、このインターフェイスのメソッドを呼び出して、ターゲットプロセス内のメモリおよびその他のデータにアクセスします。  
  
- デバッガークライアントは、特定のターゲット (ライブプロセスやメモリダンプなど) に適した方法でこのインターフェイスを実装する必要があります。  
  
- メソッド`ICorDebugDataTarget`を呼び出すことができるのは、他の`ICorDebug*`インターフェイスで実装されているメソッド内からだけです。 これにより、デバッガークライアントは、呼び出されるスレッドとそのタイミングを制御できます。  
  
- 実装`ICorDebugDataTarget`では、常にターゲットに関する最新の情報を返す必要があります。  
  
 ターゲットプロセスは、インターフェイス (および`ICorDebug*` `ICorDebugDataTarget`メソッド) が呼び出されている間は停止し、変更されないようにする必要があります。 ターゲットがライブプロセスであり、その状態が変更された場合、 [ICLRDebugging:: OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md)メソッドを再度呼び出して、置換されたののインスタンスを提供する必要があります。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
