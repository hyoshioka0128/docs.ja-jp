---
title: トレースおよびデバッグ設定のスキーマ
ms.date: 03/30/2017
helpviewer_keywords:
- tracing [.NET Framework], trace and debug settings schema
- configuration schema [.NET Framework], trace and debug settings
- configuration settings [.NET Framework], tracing
- schema configuration settings
- configuration settings [.NET Framework], debugging
- trace listeners, trace and debug settings schema
- configuration sections [.NET Framework]
- elements [.NET Framework], trace and debug settings
ms.assetid: 277ca5f6-e1c4-41b6-a47f-3a67ce5b94ac
ms.openlocfilehash: 037d08b33e9aa6a64d236b36ebcf821b604b03df
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69927119"
---
# <a name="trace-and-debug-settings-schema"></a>トレースおよびデバッグ設定のスキーマ
トレースおよびデバッグの設定により、メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。  
  
 次の表に、トレース設定とデバッグ設定の各要素の機能を示します。  
  
|要素|説明|  
|-------------|-----------------|  
|[\<add>](add-element-for-listeners-for-source.md)|トレース ソースの `Listeners` コレクションにリスナーを追加します。|  
|[\<add>](add-element-for-listeners-for-trace.md)|`Listeners` コレクションにリスナーを追加します。|  
|[\<add>](add-element-for-sharedlisteners.md)|`sharedListeners` コレクションにリスナーを追加します。|  
|[\<add>](add-element-for-switches.md)|トレース スイッチを設定するレベルを指定します。|  
|[\<assert>](assert-element.md)|<xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> メソッドの呼び出し時にメッセージ ボックスを表示するかどうかを指定し、メッセージの書き込み先のファイルの名前も指定します。|  
|[\<clear>](clear-element-for-listeners-for-source.md)|トレース ソースの `Listeners` コレクションを消去します。|  
|[\<clear>](clear-element-for-listeners-for-trace.md)|トレースの `Listeners` コレクションを削除します。|  
|[\<filter>](filter-element-for-add-for-listeners-for-source.md)|トレース ソースの `Listeners` コレクション内のリスナーにフィルターを追加します。|  
|[\<filter>](filter-element-for-add-for-listeners-for-trace.md)|トレースの `Listeners` コレクションのリスナーにフィルターに追加します。|  
|[\<filter>](filter-element-for-add-for-sharedlisteners.md)|`sharedListeners` コレクションのリスナーにフィルターを追加します。|  
|[\<listeners>](listeners-element-for-source.md)|トレース ソースの `Listeners` コレクションにリスナーを指定します。|  
|[\<listeners>](listeners-element-for-trace.md)|トレースの `Listeners` コレクションにリスナーを指定します。|  
|[\<performanceCounters>](performancecounters-element.md)|パフォーマンス カウンターが共有するグローバル メモリのサイズを指定します。|  
|[\<remove>](remove-element-for-listeners-for-trace.md)|トレースの `Listeners` コレクションからリスナーを削除します。|  
|[\<remove>](remove-element-for-listeners-for-source.md)|トレース ソースの `Listeners` コレクションからリスナーを削除します。|  
|[\<sharedListeners>](sharedlisteners-element.md)|任意の source 要素または trace 要素が参照できるリスナーを含みます。|  
|[\<sources>](sources-element.md)|トレース メッセージを開始するトレース ソースを保持します。|  
|[\<source>](source-element.md)|トレース メッセージを開始するトレース ソースを指定します。|  
|[\<switches>](switches-element.md)|トレース スイッチと、トレース スイッチを設定するレベルを保持します。|  
|[\<system.diagnostics>](system-diagnostics-element.md)|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|[\<trace>](trace-element.md)|トレース メッセージを収集、格納、およびルーティングするリスナーを保持します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.Debug>
- [構成ファイル スキーマ](../index.md)
