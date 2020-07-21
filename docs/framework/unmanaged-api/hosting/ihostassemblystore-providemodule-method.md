---
title: IHostAssemblyStore::ProvideModule メソッド
ms.date: 03/30/2017
api_name:
- IHostAssemblyStore.ProvideModule
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyStore::ProvideModule
helpviewer_keywords:
- IHostAssemblyStore::ProvideModule method [.NET Framework hosting]
- ProvideModule method [.NET Framework hosting]
ms.assetid: f42e3dd0-c88e-4748-b6c0-4c515a633180
topic_type:
- apiref
ms.openlocfilehash: 002f4177f19c2aae99e91e3fe1029b81e17481dc
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83805014"
---
# <a name="ihostassemblystoreprovidemodule-method"></a>IHostAssemblyStore::ProvideModule メソッド
アセンブリ内のモジュール、またはリンクされている (埋め込みではない) リソースファイル内のモジュールを解決します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ProvideModule (  
    [in]  ModuleBindInfo *pBindInfo,  
    [out] DWORD          *pdwModuleId,  
    [out] IStream        **ppStmModuleImage,  
    [out] IStream        **ppStmPDB  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pBindInfo`  
 から要求されたモジュールの、アセンブリ、およびモジュール名を記述する[Modulebindinfo](modulebindinfo-structure.md)インスタンスへのポインター <xref:System.AppDomain> 。  
  
 `pdwModuleId`  
 入出力読み込まれたモジュールを格納しているの一意の識別子へのポインター `IStream` 。  
  
 `ppStmModuleImage`  
 入出力読み込み対象の `IStream` ポータブル実行可能 (PE) イメージを格納しているオブジェクトのアドレスへのポインター。モジュールが見つからなかった場合は null。  
  
 `ppStmPDB`  
 入出力`IStream`要求されたモジュールのプログラムデバッグ (PDB) 情報を格納しているオブジェクトのアドレスへのポインター、または .pdb ファイルが見つからなかった場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`ProvideModule`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|COR_E_FILENOTFOUND (0x80070002)|要求されたアセンブリまたはリンクされたリソースが見つかりませんでした。|  
|E_NOT_SUFFICIENT_BUFFER|`pdwModuleId`は、ホストが返す識別子を格納するのに十分な大きさではありません。|  
  
## <a name="remarks"></a>解説  
 に対して返される id 値 `pdwModuleId` は、ホストによって指定されます。 識別子は、プロセスの有効期間内で一意である必要があります。 CLR は、この値を、関連付けられているストリームの一意の識別子として使用します。 これは、各値を、の `pAssemblyId` 呼び出しによって返された値と比較し[、の](ihostassemblystore-provideassembly-method.md) `pdwModuleId` 他の呼び出しによって返された値と比較して確認 `ProvideModule` します。 ホストが別のと同じ識別子の値を返した場合、 `IStream` CLR は、そのストリームの内容が既にマップされているかどうかを確認します。 その場合、CLR は新しいイメージをマップするのではなく、イメージの既存のコピーを読み込みます。 したがって、識別子も、から返されるアセンブリ識別子と重複しないようにする必要があり `ProvideAssembly` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager インターフェイス](ihostassemblymanager-interface.md)
- [IHostAssemblyStore インターフェイス](ihostassemblystore-interface.md)
