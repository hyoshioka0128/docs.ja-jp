---
title: ICLRDataTarget インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRDataTarget
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget
helpviewer_keywords:
- ICLRDataTarget interface [.NET Framework debugging]
ms.assetid: e2f05155-9bef-4e11-b703-7f05890665ca
topic_type:
- apiref
ms.openlocfilehash: 30806394a8895084068acaec6f7d03c6b67bb14b
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860566"
---
# <a name="iclrdatatarget-interface"></a>ICLRDataTarget インターフェイス
共通言語ランタイム (CLR) のターゲット項目と対話するためのメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|Method|説明|  
|------------|-----------------|  
|[GetCurrentThreadID メソッド](iclrdatatarget-getcurrentthreadid-method.md)|現在のスレッドのオペレーティングシステム id を取得します。|  
|[GetImageBase メソッド](iclrdatatarget-getimagebase-method.md)|指定したイメージのベースメモリアドレスを取得します。|  
|[GetMachineType メソッド](iclrdatatarget-getmachinetype-method.md)|ターゲットプロセスが使用している命令セットの種類の識別子を取得します。|  
|[GetPointerSize メソッド](iclrdatatarget-getpointersize-method.md)|現在のターゲットへのポインターのサイズ (バイト単位) を取得します。|  
|[GetThreadContext メソッド](iclrdatatarget-getthreadcontext-method.md)|指定した識別子を持つスレッドのコンテキストへのポインターを取得します。|  
|[GetTLSValue メソッド](iclrdatatarget-gettlsvalue-method.md)|指定したスレッドの指定したインデックスにあるスレッドローカルストレージ (TLS) の値を取得します。|  
|[ReadVirtual メソッド](iclrdatatarget-readvirtual-method.md)|指定された仮想メモリアドレスから指定されたバッファーにデータを読み取ります。|  
|[要求メソッド](iclrdatatarget-request-method.md)|実装で定義されているように、操作を要求するために、共通言語ランタイム (CLR) データアクセスサービスによって呼び出されます。|  
|[SetThreadContext メソッド](iclrdatatarget-setthreadcontext-method.md)|ターゲットプロセス内の指定されたスレッドの現在のコンテキストを設定します。|  
|[SetTLSValue メソッド](iclrdatatarget-settlsvalue-method.md)|ターゲットプロセス内の指定したスレッドのスレッドローカルストレージ (TLS) の値を設定します。|  
|[WriteVirtual メソッド](iclrdatatarget-writevirtual-method.md)|指定されたバッファーから指定された仮想メモリアドレスにデータを書き込みます。|  
  
## <a name="remarks"></a>解説  
 API クライアント (つまり、デバッガー) は、特定のターゲット項目に適した方法でこのインターフェイスを実装する必要があります。 たとえば、ライブ プロセスの実装は、メモリ ダンプの実装とは異なります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataTarget2 インターフェイス](iclrdatatarget2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
