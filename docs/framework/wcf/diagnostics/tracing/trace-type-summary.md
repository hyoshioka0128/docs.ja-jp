---
title: トレースの種類の概要
ms.date: 03/30/2017
ms.assetid: e639410b-d1d1-479c-b78e-a4701d4e4085
ms.openlocfilehash: 8ed6dceb19caa52f928f285064c60337e3f15a87
ms.sourcegitcommit: 515469828d0f040e01bde01df6b8e4eb43630b06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78674836"
---
# <a name="trace-type-summary"></a>トレースの種類の概要
[ソースレベルは](xref:System.Diagnostics.SourceLevels)、さまざまなトレースレベルを定義します:クリティカル、エラー、警告、情報、および詳細、およびトレース境界とアクティビティ転送`ActivityTracing`イベントの出力を切り替えるフラグの説明を提供します。  
  
 から出力できるトレース<xref:System.Diagnostics.TraceEventType>の種類を確認することもできます<xref:System.Diagnostics>。  
  
 最も重要な種類を次の表に示します。  
  
|トレースの種類|説明|  
|----------------|-----------------|  
|Critical|致命的なエラーまたはアプリケーションのクラッシュ。|  
|エラー|回復可能なエラー。|  
|警告|情報メッセージです。|  
|Information|重大ではない問題。|  
|"詳細"|トレースのデバッグ。|  
|[開始]|処理の論理単位の開始。|  
|[中断]|処理の論理単位の中断。|  
|Resume|処理の論理単位の再開。|  
|Stop|処理の論理単位の停止。|  
|転送|相関 ID の変更。|  
  
 アクティビティは、上記のトレースの種類の組み合わせとして定義されます。  
  
 ローカル (トレース ソース) スコープでの典型的なアクティビティを定義する正規表現は次のとおりです。  
  
 `R = Start (Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop`  
  
 これは、アクティビティが次の条件を満たす必要があることを意味します。  
  
- アクティビティは、Start トレースによって開始し、Stop トレースによって停止する必要があります。  
  
- Suspend トレースまたは Resume トレースの直前に Transfer トレースが必要です。  
  
- Suspend トレースと Resume トレースが存在する場合、これらのトレースの間にトレースが存在することはできません。  
  
- 上記の条件を満たしている限り、Critical/Error/Warning/Information/Verbose/Transfer の各トレースはいくつでも含めることができます。  
  
 グローバル スコープでの典型的なアクティビティを定義する正規表現は次のとおりです。  
  
`R+`  
  
 R はローカル スコープのアクティビティを表す正規表現です。 これは、次のようになります。  
  
`[R+ = Start ( Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop]+`
