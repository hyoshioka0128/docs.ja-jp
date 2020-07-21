---
title: ICLRRuntimeInfo::GetInterface メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetInterface
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetInterface
helpviewer_keywords:
- GetInterface method [.NET Framework hosting]
- ICLRRuntimeInfo::GetInterface method [.NET Framework hosting]
ms.assetid: cc7b0e5b-48c3-4509-8ebb-611ddb1f7ec2
topic_type:
- apiref
ms.openlocfilehash: 9cf9d48bf50ffc1fc56270c13215acfef6d9c3af
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504057"
---
# <a name="iclrruntimeinfogetinterface-method"></a>ICLRRuntimeInfo::GetInterface メソッド
現在のプロセスに CLR を読み込み、 [ICLRRuntimeHost](iclrruntimehost-interface.md)、 [ICLRStrongName](iclrstrongname-interface.md)、 [IMetaDataDispenserEx](../metadata/imetadatadispenser-interface.md)などのランタイムインターフェイスポインターを返します。  
  
 このメソッドは、 `CorBindTo` 「[非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)」セクションのすべての * 関数を置き換えます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetInterface(  
[in]  REFCLSID rclsid,  
[in]  REFIID   riid,  
[out, iid_is(riid), retval] LPVOID *ppUnk);  
```  
  
## <a name="parameters"></a>パラメーター  
 `rclsid`  
 からコクラスの CLSID インターフェイス。  
  
 `riid`  
 から要求されたインターフェイスの IID `rclsid` 。  
  
 `ppUnk`  
 入出力クエリされたインターフェイスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`ppUnk` が null です。|  
|E_OUTOFMEMORY|要求を処理するのに十分なメモリがありません。|  
|CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND|以前の CLR バージョン2のアクティブ化ポリシーに、別のランタイムが既にバインドされています。|  
  
## <a name="remarks"></a>解説  
 このメソッドを使用すると、CLR が読み込まれますが、初期化されません。  
  
 次の表は、とでサポートされている組み合わせを示して `rclsid` `riid` います。  
  
|`rclsid`|`riid`|  
|--------------|------------|  
|CLSID_CorMetaDataDispenser|IID_IMetaDataDispenser、IID_IMetaDataDispenserEx|  
|CLSID_CorMetaDataDispenserRuntime|IID_IMetaDataDispenser、IID_IMetaDataDispenserEx|  
|CLSID_CorRuntimeHost|IID_ICorRuntimeHost|  
|CLSID_CLRRuntimeHost|IID_ICLRRuntimeHost|  
|CLSID_TypeNameFactory|IID_ITypeNameFactory|  
|CLSID_CLRDebuggingLegacy|IID_ICorDebug|  
|||  
|CLSID_CLRStrongName|IID_ICLRStrongName|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
