---
title: ネットワークのトレースの有効化
description: .NET Framework でマネージド アプリケーションに対するメソッド呼び出しおよびネットワーク トラフィックについての情報を提供する、ネットワークのトレースを有効にする方法について学習します。
ms.date: 03/30/2017
helpviewer_keywords:
- trace destinations
- sending traces to log file
- trace listeners, network tracing
- network tracing, enabling
- CLR Debugger
- default listeners
- logs, trace
- destination for tracing output
ms.assetid: 5fff458c-51a6-4134-ba47-8a6137ddc41e
ms.openlocfilehash: 4ad0b23fc93ddcdc11cebcc556d12148df5e8ae2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502601"
---
# <a name="enabling-network-tracing"></a>ネットワークのトレースの有効化
ネットワークのトレースでは、メソッド呼び出しについての情報、およびマネージド アプリケーションによって生成されるネットワーク トラフィックについての情報にアクセスできます。 アプリケーションでネットワーク トレースを有効にするには、次のタスクを実行する必要があります。  
  
- トレースを有効にしてコードをコンパイルします。 「[方法:トレースとデバッグを指定して条件付きコンパイルを実行する](../debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)」で、トレースを有効にするために必要なコンパイラ スイッチの詳細を参照してください。  
  
- トレースの出力先を指定します。  
  
- ネットワークのトレースの動作を構成します。 「[方法:ネットワークのトレースを構成する](how-to-configure-network-tracing.md)」で、詳細を参照してください。  
  
 最も一般的なトレース先 (トレース リスナーとも呼ばれます) は、既定のリスナーとログ ファイルです。  
  
 トレース リスナーを指定しない場合、トレースは既定のリスナーを使用します。 .NET Framework SDK に付属の CLR デバッガーや、Windows SDK に付属の DBwin32.exe などのマネージド コード対応のデバッガーでコードを実行することで、既定のリスナーに送信されたメッセージを表示することができます。 CLR デバッガーを使用すると、 **[出力]** ウィンドウにトレース メッセージが表示されます。  
  
 ファイルを使用してトレースを受信する場合は、次の例のように、構成設定を使用して、ログ ファイルを指定できます (構成ファイルに関する全般的な説明については、「[構成ファイル](../configure-apps/index.md)」を参照してください)。  
  
 トレースをログ ファイルに送信するには、次のノードを適切な (アプリケーションまたはコンピューターの) 構成ファイルの `<system.diagnostics>` ノードに追加します。 必要に応じてファイルの名前 (trace.log) を変更することができます。  
  
```xml  
<system.diagnostics>  
  <trace autoflush="true" indentsize="4">  
    <listeners>  
      <add name="file" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log"/>  
    </listeners>
  </trace>  
</system.diagnostics>  
```  
  
## <a name="see-also"></a>関連項目

- [ネットワークのトレースの解釈](interpreting-network-tracing.md)
- [.NET Framework のネットワークのトレース](network-tracing.md)
- [アプリケーションのトレースとインストルメント](../debug-trace-profile/tracing-and-instrumenting-applications.md)
