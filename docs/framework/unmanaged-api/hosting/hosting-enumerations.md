---
title: ホスティングの列挙体
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged enumerations [.NET Framework], hosting
- enumerations [.NET Framework hosting]
- hosting enumerations [.NET Framework]
ms.assetid: e09131eb-1f7d-4f52-ae42-7393e9b62ef6
ms.openlocfilehash: 8edace3191ee4477b19f199d5db6c891c993dcd5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504304"
---
# <a name="hosting-enumerations"></a>ホスティングの列挙体
このセクションでは、ホスティング API が使用するアンマネージ列挙について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [CLSID_RESOLUTION_FLAGS 列挙型](clsid-resolution-flags-enumeration.md)  
 共通言語ランタイム (CLR: common language runtime) でを解決する方法を示す値を格納し `CLSID` ます。  
  
 [COR_GC_STAT_TYPES 列挙体](cor-gc-stat-types-enumeration.md)  
 ガベージコレクション用に記録する統計を指定します。  
  
 [COR_GC_THREAD_STATS_TYPES 列挙体](cor-gc-thread-stats-types-enumeration.md)  
 スレッドのガベージコレクションの統計を示します。  
  
 [EApiCategories 列挙型](eapicategories-enumeration.md)  
 部分的に信頼されたコードでホストが実行をブロックできる機能のカテゴリについて説明します。  
  
 [EBindPolicyLevels 列挙型](ebindpolicylevels-enumeration.md)  
 アセンブリポリシーを適用または変更するレベルを指定するフラグを提供します。  
  
 [ECLRAssemblyIdentityFlags 列挙型](eclrassemblyidentityflags-enumeration.md)  
 アセンブリの id の種類を示します。  
  
 [EClrEvent 列挙型](eclrevent-enumeration.md)  
 ホストがコールバックを登録できる CLR イベントについて説明します。  
  
 [EClrFailure 列挙型](eclrfailure-enumeration.md)  
 ホストがポリシーアクションを設定できるエラーのセットについて説明します。  
  
 [EClrOperation 列挙型](eclroperation-enumeration.md)  
 ホストがポリシーアクションを適用できる操作のセットについて説明します。  
  
 [EClrUnhandledException 列挙型](eclrunhandledexception-enumeration.md)  
 ユーザーコードで処理されない例外を管理するために使用できるオプションについて説明します。  
  
 [EContextType 列挙型](econtexttype-enumeration.md)  
 現在実行中のスレッドのセキュリティコンテキストを記述します。  
  
 [ECustomDumpFlavor 列挙型](ecustomdumpflavor-enumeration.md)  
 エラーを報告するときに、ヒープダンプのカスタムサブセットに含めるアイテムを示す値を格納します。  
  
 [ECustomDumpItemKind 列挙型](ecustomdumpitemkind-enumeration.md)  
 [Customdumpitem 構造](customdumpitem-structure.md)体の将来の拡張のために予約されています。  
  
 [EHostApplicationPolicy 列挙型](ehostapplicationpolicy-enumeration.md)  
 [IHostAssemblyManager interface](ihostassemblymanager-interface.md)インターフェイスオブジェクトを変更する方法を示します。 この列挙型は非推奨とされました。  
  
 [EHostBindingPolicyModifyFlags 列挙型](ehostbindingpolicymodifyflags-enumeration.md)  
 ソースアセンブリからターゲットアセンブリにポリシー変更を適用するときに、CLR が実行する必要のあるリダイレクトの種類をホストが指定できるようにします。  
  
 [EInitializeNewDomainFlags 列挙体](einitializenewdomainflags-enumeration.md)  
 ホストがアプリケーションドメインの初期化に関する情報をランタイムに提供できるようにします。  
  
 [EMemoryAvailable 列挙型](ememoryavailable-enumeration.md)  
 コンピューターの空き物理メモリの量を示す値を格納します。  
  
 [EMemoryCriticalLevel 列挙型](ememorycriticallevel-enumeration.md)  
 特定のメモリ割り当てが要求されたが、満たされない場合のエラーの影響を示す値を格納します。  
  
 [EPolicyAction 列挙型](epolicyaction-enumeration.md)  
 [EClrOperation 列挙](eclroperation-enumeration.md)によって記述される操作と、 [Eclrfailure 列挙](eclrfailure-enumeration.md)によって記述されるエラーについて、ホストが設定できるポリシーアクションについて説明します。  
  
 [ESymbolReadingPolicy 列挙型](esymbolreadingpolicy-enumeration.md)  
 プログラムデータベース (PDB) ファイルを読み取るためのポリシーを設定する値が含まれます。  
  
 [ETaskType 列挙型](etasktype-enumeration.md)  
 [ICLRTask インターフェイス](iclrtask-interface.md)または[IHostTask](ihosttask-interface.md)インターフェイスインターフェイスによって表されるタスクの種類を示す値を格納します。  
  
 [HOST_TYPE 列挙型](host-type-enumeration.md)  
 アプリケーションを起動しているホストの種類を指定する値を格納します。  
  
 [MALLOC_TYPE 列挙体](malloc-type-enumeration.md)  
 割り当てられているメモリの特性を指定する値を格納します。  
  
 [METAHOST_CONFIG_FLAGS 列挙体](metahost-config-flags-enumeration.md)  
 `pdwConfigFlags` [ICLRMetaHostPolicy:: GetRequestedRuntime](iclrmetahostpolicy-getrequestedruntime-method.md)メソッドのパラメーターで返されるフラグについて説明します。  
  
 [METAHOST_POLICY_FLAGS 列挙体](metahost-policy-flags-enumeration.md)  
 ほとんどのランタイムホストに共通のバインドポリシーを提供します。  
  
 [RUNTIME_INFO_FLAGS 列挙型](runtime-info-flags-enumeration.md)  
 CLR に関する情報を返す必要があるかどうかを示す値を格納します。  
  
 [StackOverflowType 列挙型](stackoverflowtype-enumeration.md)  
 スタックオーバーフローイベントの根底にある原因を示す値を格納します。  
  
 [STARTUP_FLAGS 列挙型](startup-flags-enumeration.md)  
 CLR のスタートアップ動作を示す値を格納します。  
  
 [ValidatorFlags 列挙型](validatorflags-enumeration.md)  
 [Validate メソッド](iclrvalidator-validate-method.md)の呼び出しで実行する必要がある検証の種類を示す値を格納します。  
  
 [WAIT_OPTION 列挙型](wait-option-enumeration.md)  
 CLR ブロックによって要求された操作が発生した場合にホストが実行するアクションを示します。  
  
## <a name="related-sections"></a>関連項目  
 [ホスト コクラス](hosting-coclasses.md)  
  
 [ホスト インターフェイス](hosting-interfaces.md)  
  
 [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)  
  
 [ホスト構造体](hosting-structures.md)
