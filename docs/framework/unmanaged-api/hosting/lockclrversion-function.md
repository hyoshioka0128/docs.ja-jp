---
title: LockClrVersion 関数
ms.date: 03/30/2017
api_name:
- LockClrVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- LockClrVersion
helpviewer_keywords:
- LockClrVersion function [.NET Framework hosting]
ms.assetid: 1318ee37-c43b-40eb-bbe8-88fc46453d74
topic_type:
- apiref
ms.openlocfilehash: 09bcebfdcfea3d5728d404cdb6b5fb170a5432c3
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008496"
---
# <a name="lockclrversion-function"></a>LockClrVersion 関数
CLR を明示的に初期化する前に、プロセス内で使用される共通言語ランタイム (CLR) のバージョンをホストが判断できるようにします。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LockClrVersion (  
    [in] FLockClrVersionCallback   hostCallback,  
    [in] FLockClrVersionCallback  *pBeginHostSetup,  
    [in] FLockClrVersionCallback  *pEndHostSetup  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hostCallback`  
 から初期化時に CLR によって呼び出される関数。  
  
 `pBeginHostSetup`  
 から初期化を開始することを CLR に通知するために、ホストによって呼び出される関数。  
  
 `pEndHostSetup`  
 から初期化が完了したことを CLR に通知するために、ホストによって呼び出される関数。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の値に加えて、Winerror.h で定義されている標準の COM エラーコードを返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_INVALIDARG|1つ以上の引数が null です。|  
  
## <a name="remarks"></a>コメント  
 CLR を初期化する前に、ホストがを呼び出し `LockClrVersion` ます。 `LockClrVersion`は、3つのパラメーターを受け取ります。これらはすべて[Flockclrversioncallback](flockclrversioncallback-function-pointer.md)型のコールバックです。 この型は次のように定義されています。  
  
```cpp  
typedef HRESULT ( __stdcall *FLockClrVersionCallback ) ();  
```  
  
 ランタイムの初期化時には、次の手順が実行されます。  
  
1. ホストは[Corbindtoruntimeex](corbindtoruntimeex-function.md)またはその他のランタイム初期化関数のいずれかを呼び出します。 また、ホストは COM オブジェクトアクティベーションを使用してランタイムを初期化することもできます。  
  
2. ランタイムは、パラメーターによって指定された関数を呼び出し `hostCallback` ます。  
  
3. によって指定された関数は、 `hostCallback` 次の一連の呼び出しを行います。  
  
    - パラメーターによって指定された関数 `pBeginHostSetup` 。  
  
    - `CorBindToRuntimeEx`(または別のランタイム初期化関数)。  
  
    - [ICLRRuntimeHost:: SetHostControl](iclrruntimehost-sethostcontrol-method.md)。  
  
    - [ICLRRuntimeHost:: Start](iclrruntimehost-start-method.md)。  
  
    - パラメーターによって指定された関数 `pEndHostSetup` 。  
  
 からへのすべての呼び出しは、 `pBeginHostSetup` `pEndHostSetup` 同じ論理スタックを持つ1つのスレッドまたはファイバーに対して行われる必要があります。 このスレッドは、が呼び出されたときのスレッドとは異なる場合があり `hostCallback` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
