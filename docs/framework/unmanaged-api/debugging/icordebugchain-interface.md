---
title: ICorDebugChain インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugChain
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain
helpviewer_keywords:
- ICorDebugChain interface [.NET Framework debugging]
ms.assetid: f671f519-1cb3-4ae5-b9f1-abc5e783459f
topic_type:
- apiref
ms.openlocfilehash: 6ae0fec0f8de2bbe3862f9f70ed9cf3d32af34c4
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894210"
---
# <a name="icordebugchain-interface"></a>ICorDebugChain インターフェイス

物理呼び出し履歴または論理呼び出し履歴のセグメントを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumerateFrames メソッド](icordebugchain-enumerateframes-method.md)|チェーン内のすべてのマネージスタックフレームが格納された列挙子を取得します。これは、最新のフレームから始まります。|  
|[GetActiveFrame メソッド](icordebugchain-getactiveframe-method.md)|チェーンのアクティブな (つまり、最新の) フレームを取得します。|  
|[GetCallee メソッド](icordebugchain-getcallee-method.md)|このチェーンによって呼び出されたチェーンを取得します。|  
|[GetCaller メソッド](icordebugchain-getcaller-method.md)|このチェーンを呼び出したチェーンを取得します。|  
|[GetContext メソッド](icordebugchain-getcontext-method.md)|実装されていません。|  
|[GetNext メソッド](icordebugchain-getnext-method.md)|スレッドの次のフレームのチェーンを取得します。|  
|[GetPrevious メソッド](icordebugchain-getprevious-method.md)|スレッドの前のフレームのチェーンを取得します。|  
|[GetReason メソッド](icordebugchain-getreason-method.md)|この呼び出しチェーンの genesis の理由を取得します。|  
|[GetRegisterSet メソッド](icordebugchain-getregisterset-method.md)|このチェーンのアクティブな部分のレジスタセットを取得します。|  
|[GetStackRange メソッド](icordebugchain-getstackrange-method.md)|このチェーンのスタックセグメントのアドレス範囲を取得します。|  
|[GetThread メソッド](icordebugchain-getthread-method.md)|この呼び出しチェーンが含まれている物理スレッドを取得します。|  
|[IsManaged メソッド](icordebugchain-ismanaged-method.md)|このチェーンでマネージコードが実行されているかどうかを示す値を取得します。|  
  
## <a name="remarks"></a>解説  
 チェーン内のスタックフレームは、連続したスタック領域を占有し、同じスレッドとコンテキストを共有します。 チェーンは、マネージコードチェーンまたはアンマネージコードチェーンを表すことができます。 空`ICorDebugChain`のインスタンスは、アンマネージコードチェーンを表します。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
