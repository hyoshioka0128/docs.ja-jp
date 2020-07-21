---
title: CorBindToRuntimeHost 関数
ms.date: 03/30/2017
api_name:
- CorBindToRuntimeHost
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntimeHost
helpviewer_keywords:
- CorBindToRuntimeHost function [.NET Framework hosting]
ms.assetid: 5c826ba3-8258-49bc-a417-78807915fcaf
topic_type:
- apiref
ms.openlocfilehash: 9d1c7f4f5b881f7f55539602c152b557a7950472
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504408"
---
# <a name="corbindtoruntimehost-function"></a>CorBindToRuntimeHost 関数
ホストが、指定したバージョンの共通言語ランタイム (CLR: Common Language Runtime) をプロセスに読み込むことができるようにします。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CorBindToRuntimeHost (  
    [in] LPCWSTR       pwszVersion,
    [in] LPCWSTR       pwszBuildFlavor,
    [in] LPCWSTR       pwszHostConfigFile,
    [in] VOID*         pReserved,
    [in] DWORD         startupFlags,
    [in] REFCLSID      rclsid,
    [in] REFIID        riid,
    [out] LPVOID FAR  *ppv  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwszVersion`  
 [入力] 読み込む CLR のバージョンを示す文字列。  
  
 .NET Framework のバージョン番号は、ピリオドで*区切られた*4 つの部分で構成されます。 `pwszVersion` として渡される文字列は、文字 "v" で始まり、バージョン番号の最初の 3 つの部分がその後に続く必要があります (たとえば "v1.0.1529")。  
  
 いくつかのバージョンの CLR は、以前のバージョンの CLR との互換性を指定するポリシー ステートメントと共にインストールされています。 既定では、スタートアップ shim により、ポリシー ステートメントに対して `pwszVersion` が評価され、要求されたバージョンと互換性がある最新バージョンのランタイムが読み込まれます。 ホストは shim に対し、`pwszVersion` パラメーターで値 STARTUP_LOADER_SAFEMODE を渡すことにより、ポリシー評価を省略し、`startupFlags` で指定されたバージョンとまったく同じバージョンを読み込ませることができます。  
  
 `pwszVersion` が `null,` の場合、メソッドはどのバージョンの CLR も読み込みません。 代わりに、ランタイムの読み込みに失敗したことを示す CLR_E_SHIM_RUNTIMELOAD が返されます。  
  
 `pwszBuildFlavor`  
 [入力] CLR のサーバー ビルドまたはワークステーション ビルドのどちらを読み込むかを指定する文字列。 有効な値は、`svr`、`wks` です。 ワークステーション ビルドはシングルプロセッサ コンピューターでクライアント アプリケーションを実行するために最適化され、サーバー ビルドはガベージ コレクションでマルチ プロセッサを利用するために最適化されています。  
  
 `pwszBuildFlavor`が null に設定されている場合、ワークステーションのビルドが読み込まれます。 をシングルプロセッサコンピューターで実行する場合、がに設定されていても、ワークステーションのビルドは常に読み込まれ `pwszBuildFlavor` `svr` ます。 ただし、 `pwszBuildFlavor` がに設定され、 `svr` 同時実行ガベージコレクションが指定されている場合 (パラメーターの説明を参照 `startupFlags` )、サーバービルドが読み込まれます。  
  
> [!NOTE]
> 同時実行ガベージ コレクションは、Intel Itanium アーキテクチャ (以前の IA-64) を実装する 64 ビット システム上で WOW64 x86 エミュレーターを実行しているアプリケーションではサポートされません。 64ビット Windows システムでの WOW64 の使用の詳細については、「 [32 ビットアプリケーションの実行](/windows/desktop/WinProg64/running-32-bit-applications)」を参照してください。  
  
 `pwszHostConfigFile`  
 [入力] 読み込む CLR のバージョンを指定するホスト構成ファイルの名前。 ファイル名に絶対パスが含まれていない場合、ファイルは呼び出しを行った実行可能ファイルと同じディレクトリにあるものと見なされます。  
  
 `pReserved`  
 [入力] 将来の機能拡張に備えて予約されています。  
  
 `startupFlags`  
 [入力] 同時実行ガベージ コレクション、ドメインに中立なコード、および `pwszVersion` パラメーターの動作を制御するフラグのセット。 どのフラグも設定されていない場合は、既定はシングル ドメインになります。 サポートされている値の一覧については、 [STARTUP_FLAGS 列挙体](startup-flags-enumeration.md)を参照してください。  
  
 `rclsid`  
 から`CLSID` [ICorRuntimeHost](icorruntimehost-interface.md)または[ICLRRuntimeHost](iclrruntimehost-interface.md)のいずれかのインターフェイスを実装するコクラスの。 サポートされている値は CLSID_CorRuntimeHost と CLSID_CLRRuntimeHost です。  
  
 `riid`  
 [入力] 要求するインターフェイスの `IID`。 サポートされている値は IID_ICorRuntimeHost と IID_ICLRRuntimeHost です。  
  
 `ppv`  
 [出力] 読み込まれたランタイムのバージョンへのインターフェイス ポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [CorBindToCurrentRuntime 関数](corbindtocurrentruntime-function.md)
- [CorBindToRuntime 関数](corbindtoruntime-function.md)
- [CorBindToRuntimeByCfg 関数](corbindtoruntimebycfg-function.md)
- [CorBindToRuntimeEx 関数](corbindtoruntimeex-function.md)
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
