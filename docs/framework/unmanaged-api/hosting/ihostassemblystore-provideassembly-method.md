---
title: IHostAssemblyStore::ProvideAssembly メソッド
ms.date: 03/30/2017
api_name:
- IHostAssemblyStore.ProvideAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyStore::ProvideAssembly
helpviewer_keywords:
- ProvideAssembly method [.NET Framework hosting]
- IHostAssemblyStore::ProvideAssembly method [.NET Framework hosting]
ms.assetid: 625c3dd5-a3f0-442c-adde-310dadbb5054
topic_type:
- apiref
ms.openlocfilehash: 162def0d703ea81efc3df3ea5ee08b58e34822e6
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501574"
---
# <a name="ihostassemblystoreprovideassembly-method"></a>IHostAssemblyStore::ProvideAssembly メソッド
[IHostAssemblyManager:: GetNonHostStoreAssemblies](ihostassemblymanager-getnonhoststoreassemblies-method.md)から返された[ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)によって参照されていないアセンブリへの参照を取得します。 共通言語ランタイム (CLR) は、 `ProvideAssembly` 一覧に表示されない各アセンブリに対してを呼び出します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ProvideAssembly (  
    [in]  AssemblyBindInfo *pBindInfo,  
    [out] UINT64           *pAssemblyId,  
    [out] UINT64           *pHostContext,  
    [out] IStream          **ppStmAssemblyImage,  
    [out] IStream          **ppStmPDB  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pBindInfo`  
 からホストが特定のバインド特性 (バージョン管理ポリシーの有無、バインド先のアセンブリなど) を決定するために使用する[Assemblybindinfo](assemblybindinfo-structure.md)インスタンスへのポインター。  
  
 `pAssemblyId`  
 入出力このの要求されたアセンブリの一意の識別子へのポインター `IStream` 。  
  
 `pHostContext`  
 入出力プラットフォーム呼び出しを必要とせずに、要求されたアセンブリの証拠を決定するために使用されるホスト固有のデータへのポインター。 `pHostContext`<xref:System.Reflection.Assembly.HostContext%2A>マネージクラスのプロパティに対応 <xref:System.Reflection.Assembly> します。  
  
 `ppStmAssemblyImage`  
 入出力`IStream`読み込むポータブル実行可能 (PE) イメージが格納されているのアドレスへのポインター。アセンブリが見つからなかった場合は null。  
  
 `ppStmPDB`  
 入出力プログラムデバッグ (PDB) 情報を格納しているのアドレスへのポインター、 `IStream` または .pdb ファイルが見つからなかった場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`ProvideAssembly`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|COR_E_FILENOTFOUND (0x80070002)|要求されたアセンブリが見つかりませんでした。|  
|E_NOT_SUFFICIENT_BUFFER|によって指定されたバッファーサイズ `pAssemblyId` が、ホストが返す識別子を保持するのに十分な大きさではありません。|  
  
## <a name="remarks"></a>解説  
 に対して返される id 値 `pAssemblyId` は、ホストによって指定されます。 識別子は、プロセスの有効期間内で一意である必要があります。 CLR は、この値をストリームの一意の識別子として使用します。 このメソッドは、 `pAssemblyId` の他の呼び出しによって返された値と比較して、それぞれの値をチェック `ProvideAssembly` します。 ホストが別のと同じ値を返す場合、 `pAssemblyId` `IStream` CLR は、そのストリームの内容が既にマップされているかどうかをチェックします。 その場合、ランタイムは新しいイメージをマップするのではなく、イメージの既存のコピーを読み込みます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager インターフェイス](ihostassemblymanager-interface.md)
- [IHostAssemblyStore インターフェイス](ihostassemblystore-interface.md)
