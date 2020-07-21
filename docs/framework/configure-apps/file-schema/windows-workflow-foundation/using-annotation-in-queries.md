---
title: クエリにおける注釈の使用
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 50855b30-d5fe-49a9-89d3-3f1bfd670958
ms.openlocfilehash: 728408e744bc1eca62158fab1a7a17e985fe3b6c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69947284"
---
# <a name="using-annotation-in-queries"></a>クエリにおける注釈の使用
注釈を使用すると、ビルド後に構成できる値を使用して、追跡レコードへのタグ付けを任意に行うことができます。 たとえば、複数のワークフローで複数の追跡レコードを "Mail Server" = = "Mail Server1" とタグ付けすることができます。 こうすると、後で追跡レコードのクエリを実行するときに、このタグの付いたすべてのレコードを簡単に見つけることができます。  
  
## <a name="adding-annotations"></a>注釈の追加  
 次の例に示すように、追跡クエリに注釈を追加できます。  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <annotations>  
    <annotation name="MailServer" value="Mail Server1"/>  
  </annotations>  
</activityStateQuery>  
```  
  
> [!NOTE]
> これらの追跡クエリ要素は、追跡プロファイルの作成に使用できます。 追跡プロファイルは構成またはコードで作成できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ProfileWorkflowElement>
- <xref:System.Activities.Tracking.TrackingProfile>
- [\<participants>](participants.md)
- [ワークフロー追跡とトレース](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [追跡プロファイル](../../../windows-workflow-foundation/tracking-profiles.md)
