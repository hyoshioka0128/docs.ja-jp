---
title: Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
ms.date: 03/30/2017
ms.topic: reference
api_name:
- Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
api_location:
- Microsoft.VisualStudio.Activities.dll
api_type:
- Assembly
ms.assetid: 6b44b13c-7a23-4df2-8f9f-45e2b1430002
ms.openlocfilehash: 99f2eb9447bdf43cb57cfe86f35d2c09044ed470
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69947627"
---
# <a name="microsoftvisualstudioactivitiesasrclientactivitybuilderctor"></a>Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
[VisualStudio](microsoft-visualstudio-activities-asr-clientactivitybuilder.md)クラスのインスタンスを作成します。このクラスのインスタンスを作成します。  
  
## <a name="syntax"></a>構文  
  
```csharp  
public ClientActivityBuilder(OperationDescription operationDescription, string configurationName, string proxyNamespace);  
```  
  
## <a name="parameters"></a>パラメーター  
  
## <a name="parameter-values"></a>パラメーター値  
 *operationDescription*  
  
 操作名、戻り値の型、パラメーター情報など、生成されるワークフロー アクティビティで実行される操作を記述します。 このパラメーターの値を**null**にすることはできません。 これは、メッセージ コントラクトを使用し、1 つのメッセージと共に引数を受け取る同期操作を示す必要があります。 これらの条件が満たされていない場合、このクラスのコンストラクターと他のメソッドを使用したランタイムの結果は未定義です。  
  
 *configurationName*  
  
 エンドポイント構成名を指定します。 このパラメーターの値を**null**または空にすることはできません。 これらの条件が満たされていない場合、このクラスのコンストラクターと他のメソッドを使用したランタイムの結果は未定義です。  
  
 *proxyNamespace*  
  
 操作のサービスの名前空間を指定します。 このパラメーターの値を**null**または空にすることはできません。 これらの条件が満たされていない場合、このクラスのコンストラクターと他のメソッドを使用したランタイムの結果は未定義です。  
  
## <a name="see-also"></a>関連項目

- [Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder](microsoft-visualstudio-activities-asr-clientactivitybuilder.md)
