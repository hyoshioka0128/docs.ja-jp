---
title: 列挙体のプロファイリング
ms.date: 03/30/2017
helpviewer_keywords:
- profiling enumerations [.NET Framework]
- enumerations [.NET Framework profiling]
- unmanaged enumerations [.NET Framework], profiling
ms.assetid: 8d5f9570-9853-4ce8-8101-df235d5b258e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 996352637f34b0b6c0d12e611a6d9e70ab85230e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33461761"
---
# <a name="profiling-enumerations"></a>列挙体のプロファイリング
このセクションでは、プロファイル API が使用するアンマネージ列挙について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [COR_PRF_CLAUSE_TYPE 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-clause-type-enumeration.md)  
 コードが入った、または出た例外句のタイプを示します。  
  
 [COR_PRF_CODEGEN_FLAGS 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-codegen-flags-enumeration.md)  
 コード生成フラグを設定することができますを定義、 [icorprofilerfunctioncontrol::setcodegenflags](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-setcodegenflags-method.md)メソッドです。  
  
 [COR_PRF_FINALIZER_FLAGS 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-finalizer-flags-enumeration.md)  
 オブジェクトのファイナライザーを記述します。  
  
 [COR_PRF_GC_GENERATION 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-generation-enumeration.md)  
 ガベージ コレクションのジェネレーションを識別します。  
  
 [COR_PRF_GC_REASON 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-reason-enumeration.md)  
 ガベージ コレクションが発生している理由を示します。  
  
 [COR_PRF_GC_ROOT_FLAGS 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-root-flags-enumeration.md)  
 ガベージ コレクターのルートのプロパティを示します。  
  
 [COR_PRF_GC_ROOT_KIND 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-root-kind-enumeration.md)  
 によって公開されるガベージ コレクターのルートの種類を示す、 [icorprofilercallback 2::rootreferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md)コールバック。  
  
 [COR_PRF_HIGH_MONITOR 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md)  
 :Seteventmask2 フラグを提供、 [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)ために、プロファイラーが指定する列挙体、 [icorprofilerinfo 5::seteventmask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md)メソッドの読み込み時にします。  
  
 [COR_PRF_JIT_CACHE 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-jit-cache-enumeration.md)  
 キャッシュされている関数検索の結果を示します。  
  
 [COR_PRF_MISC 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-misc-enumeration.md)  
 特殊な識別子を指定する定数値を含めます。  
  
 [COR_PRF_MODULE_FLAGS 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-module-flags-enumeration.md)  
 モジュールのプロパティを指定します。  
  
 [COR_PRF_MONITOR 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)  
 プロファイラーがサブスクライブしようとする動作、機能、またはイベントの指定で使用する値を含めます。  
  
 [COR_PRF_RUNTIME_TYPE 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-runtime-type-enumeration.md)  
 共通言語ランタイムのバージョンを表す値を含めます。  
  
 [COR_PRF_SNAPSHOT_INFO 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-snapshot-info-enumeration.md)  
 プロファイラーの `StackSnapshotCallback` 関数への各呼び出しにおいて、スタック スナップショットでどのくらいのデータが返されるかを指定します。  
  
 [COR_PRF_STATIC_TYPE 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-static-type-enumeration.md)  
 フィールドが静的であるかどうかを示し、静的な場合は、フィールドに適用される静的なクオリティを示します。  
  
 [COR_PRF_SUSPEND_REASON 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-suspend-reason-enumeration.md)  
 ランタイムが中断された理由を示します。  
  
 [COR_PRF_TRANSITION_REASON 列挙型](../../../../docs/framework/unmanaged-api/profiling/cor-prf-transition-reason-enumeration.md)  
 マネージ コードからアンマネージ コードへ、またはその逆の遷移の理由を示します。  
  
## <a name="related-sections"></a>関連項目  
 [プロファイルの概要](../../../../docs/framework/unmanaged-api/profiling/profiling-overview.md)  
  
 [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
  
 [グローバル静的関数のプロファイル](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)  
  
 [構造体のプロファイリング](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
