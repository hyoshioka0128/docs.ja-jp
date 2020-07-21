---
title: ICLRMetaHost::RequestRuntimeLoadedNotification メソッド
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::RequestRuntimeLoadedNotification
helpviewer_keywords:
- RequestRuntimeLoadedNotification method [.NET Framework hosting]
- ICLRMetaHost::RequestRuntimeLoadedNotification method [.NET Framework hosting]
ms.assetid: 0d5ccc4d-0193-41f5-af54-45d7b70d5321
topic_type:
- apiref
ms.openlocfilehash: 6813f72f9d27aeff90f797a6ca9370b22e03e6f0
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703695"
---
# <a name="iclrmetahostrequestruntimeloadednotification-method"></a>ICLRMetaHost::RequestRuntimeLoadedNotification メソッド
共通言語ランタイム (CLR) のバージョンが最初に読み込まれたが、まだ開始されていないときに呼び出されることが保証されているコールバック関数を提供します。 このメソッドは、 [Lockclrversion](lockclrversion-function.md)関数よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RequestRuntimeLoadedNotification (  
    [in] RuntimeLoadedCallbackFnPtr pCallbackFunction);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pCallbackFunction`  
 から新しいランタイムが読み込まれたときに呼び出されるコールバック関数。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pCallbackFunction` が null です。|  
  
## <a name="remarks"></a>解説  
 コールバックは、次のように機能します。  
  
- コールバックは、ランタイムが初めて読み込まれるときにのみ呼び出されます。  
  
- 同じランタイムの再入可能な読み込みに対してコールバックが呼び出されません。  
  
- 再入可能でないランタイムの読み込みでは、コールバック関数の呼び出しがシリアル化されます。  
  
 コールバック関数のプロトタイプは次のとおりです。  
  
```cpp  
typedef void (__stdcall *RuntimeLoadedCallbackFnPtr)(  
                     ICLRRuntimeInfo *pRuntimeInfo,  
                     CallbackThreadSetFnPtr pfnCallbackThreadSet,  
                     CallbackThreadUnsetFnPtr pfnCallbackThreadUnset);  
```  
  
 コールバック関数のプロトタイプは次のとおりです。  
  
- `pfnCallbackThreadSet`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadSetFnPtr)();  
    ```  
  
- `pfnCallbackThreadUnset`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadUnsetFnPtr)();  
    ```  
  
 ホストの読み込みまたは再入によって別のランタイムの読み込みが発生する場合は、 `pfnCallbackThreadSet` `pfnCallbackThreadUnset` コールバック関数で指定されたパラメーターとパラメーターを次のように使用する必要があります。  
  
- `pfnCallbackThreadSet`このような読み込みが試行される前に、ランタイムの読み込みを発生させる可能性のあるスレッドによって呼び出される必要があります。  
  
- `pfnCallbackThreadUnset`は、スレッドがこのようなランタイム読み込みを行わなくなる場合 (および最初のコールバックから戻る前) に呼び出す必要があります。  
  
- `pfnCallbackThreadSet`と `pfnCallbackThreadUnset` はどちらも再入不可能です。  
  
> [!NOTE]
> ホストアプリケーションは、 `pfnCallbackThreadSet` `pfnCallbackThreadUnset` パラメーターのスコープ外でおよびを呼び出すことはできません `pCallbackFunction` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRMetaHost インターフェイス](iclrmetahost-interface.md)
- [ホスティング](index.md)
