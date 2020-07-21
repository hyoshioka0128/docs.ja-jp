---
title: .NET Framework 4 および 4.5 で追加された CLR ホスト インターフェイス
ms.date: 03/30/2017
helpviewer_keywords:
- hosting interfaces [.NET Framework], version 4
- .NET Framework 4, hosting interfaces
- interfaces [.NET Framework hosting], version 4
ms.assetid: f6af6116-f5b0-4bda-a276-fffdba70893d
ms.openlocfilehash: a524c0b0e01fbde95ce2341874511960b3e5738e
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616854"
---
# <a name="clr-hosting-interfaces-added-in-the-net-framework-4-and-45"></a>.NET Framework 4 および 4.5 で追加された CLR ホスト インターフェイス
ここでは、アンマネージホストが .NET Framework 4、.NET Framework 4.5、およびそれ以降のバージョンの共通言語ランタイム (CLR) をアプリケーションに統合するために使用できるインターフェイスについて説明します。 これらのインターフェイスは、ホストがランタイムを構成してプロセスに読み込むためのメソッドを提供します。  
  
 .NET Framework 4 以降では、すべてのホストインターフェイスに次の特性があります。  
  
- これらは、有効期間管理 ( `AddRef` および `Release` )、カプセル化 (暗黙的なコンテキスト)、および `QueryInterface` COM からの使用を行います。  
  
- これらの型は `BSTR` 、、、などの COM 型を使用しません `SAFEARRAY` `VARIANT` 。  
  
- [CoCreateInstance 関数](/windows/win32/api/combaseapi/nf-combaseapi-cocreateinstance)を使用するアパートメントモデル、集計、またはレジストリのアクティブ化はありません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ICLRAppDomainResourceMonitor インターフェイス](iclrappdomainresourcemonitor-interface.md)  
 アプリケーションドメインのメモリおよび CPU 使用率を検査するメソッドを提供します。  
  
 [ICLRDomainManager インターフェイス](iclrdomainmanager-interface.md)  
 既定のアプリケーションドメインを初期化し、初期化プロパティを指定するために使用されるアプリケーションドメインマネージャーをホストが指定できるようにします。  
  
 [ICLRGCManager2 インターフェイス](iclrgcmanager2-interface.md)  
 [SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md)メソッドを提供します。これにより、ホストはガベージコレクションセグメントのサイズとガベージコレクションシステムのジェネレーション0の最大サイズをより大きい値に設定でき `DWORD` ます。  
  
 [ICLRMetaHost インターフェイス](iclrmetahost-interface.md)  
 特定のバージョンの CLR を返し、インストールされているすべての CLRs の一覧を取得し、すべてのインプロセスランタイムを一覧表示し、アクティベーションインターフェイスを返し、アセンブリをコンパイルするために使用される CLR バージョンを検出するメソッドを提供します。  
  
 [ICLRMetaHostPolicy インターフェイス](iclrmetahostpolicy-interface.md)  
 ポリシー条件、マネージアセンブリ、バージョン、および構成ファイルに基づいて CLR インターフェイスを提供する[Getrequestedruntime](iclrmetahostpolicy-getrequestedruntime-method.md)メソッドを提供します。  
  
 [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)  
 バージョン、ディレクトリ、読み込みステータスなど、特定のランタイムに関する情報を返すメソッドを提供します。  
  
 [ICLRStrongName インターフェイス](iclrstrongname-interface.md)  
 厳密な名前でアセンブリに署名するための基本的なグローバル静的関数を提供します。 すべての[ICLRStrongName](iclrstrongname-interface.md)メソッドは、標準 COM hresult を返します。  
  
 [ICLRStrongName2 インターフェイス](iclrstrongname2-interface.md)  
 セキュリティで保護されたハッシュアルゴリズム (SHA-256、SHA-384、および SHA-512) の SHA-1 グループを使用して、厳密な名前を作成する機能を提供します。  
  
 [ICLRTask2 インターフェイス](iclrtask2-interface.md)  
 には、 [ICLRTask インターフェイス](iclrtask-interface.md)のすべての機能が用意されています。また、には、現在のスレッドでスレッドの中止を遅延させることができるメソッドが用意されています。  
  
## <a name="related-sections"></a>関連項目  
 [非推奨の CLR のホスト インターフェイスおよびコクラス](deprecated-clr-hosting-interfaces-and-coclasses.md)  
 .NET Framework バージョン1.0 および1.1 で提供されるホストインターフェイスについて説明します。  
  
 [CLR ホスト インターフェイス](clr-hosting-interfaces.md)  
 .NET Framework バージョン2.0、3.0、および3.5 で提供されるホストインターフェイスについて説明します。  
  
 [ホスティング](index.md)  
 .NET Framework でのホスティングについて説明します。
