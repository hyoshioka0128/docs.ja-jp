---
title: ICLRDataTarget2::AllocVirtual メソッド
ms.date: 03/30/2017
api_name:
- ICLRDataTarget2.AllocVirtual
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget2::AllocVirtual
helpviewer_keywords:
- ICLRDataTarget2::AllocVirtual method [.NET Framework debugging]
- AllocVirtual method [.NET Framework debugging]
ms.assetid: e3226230-964b-47fb-9f53-d6fdbeda1e9e
topic_type:
- apiref
ms.openlocfilehash: 20b73549d30fe210e4d44902d2f459ea9c682360
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860486"
---
# <a name="iclrdatatarget2allocvirtual-method"></a>ICLRDataTarget2::AllocVirtual メソッド
このターゲットプロセスのアドレス空間にメモリを割り当てるために、共通言語ランタイム (CLR) データアクセスサービスによって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AllocVirtual(  
    [in] CLRDATA_ADDRESS addr,  
    [in] ULONG32 size,  
    [in] ULONG32 typeFlags,  
    [in] ULONG32 protectFlags,  
    [out] CLRDATA_ADDRESS* virt  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `addr`  
 から割り当て`CLRDATA_ADDRESS`られるメモリの、要求された開始アドレスを示す値です。  
  
 `size`  
 から割り当てるメモリのサイズ (バイト単位)。  
  
 `typeFlags`  
 からメモリの割り当てを制御するフラグ。 Win32 `VirtualAlloc`関数を参照してください。  
  
 `protectFlags`  
 から割り当てられたメモリの保護属性。 Win32 `VirtualAlloc`関数を参照してください。  
  
 `virt`  
 入出力割り当てられた`CLRDATA_ADDRESS`メモリの実際の開始アドレスを指定する値へのポインター。  
  
## <a name="remarks"></a>解説  
 この`AllocVirtual`メソッドは、Win32 `VirtualAlloc`関数の論理ラッパーとして機能します。  
  
 このメソッドは、デバッグ アプリケーションの作成者によって実装されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataTarget2 インターフェイス](iclrdatatarget2-interface.md)
- [FreeVirtual メソッド](iclrdatatarget2-freevirtual-method.md)
