---
title: 1150 - CompensationState
ms.date: 03/30/2017
ms.assetid: eb015842-cc5a-47be-bce5-6af39e567723
ms.openlocfilehash: 61613a27c4d4d8fb0b206246fef25ae87def47a5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33510682"
---
# <a name="1150---compensationstate"></a>1150 - CompensationState
## <a name="properties"></a>プロパティ  
  
|||  
|-|-|  
|ID|1150|  
|キーワード|WFActivities|  
|レベル|情報|  
|チャネル|Microsoft-Windows-Application Server-Applications/Debug|  
  
## <a name="description"></a>説明  
 CompensableActivity の状態の変更を示します。  
  
## <a name="message"></a>メッセージ  
 CompensableActivity '%1' は '%2' 状態です。  
  
## <a name="details"></a>詳細  
  
|データ項目名|データ項目の型|説明|  
|--------------------|--------------------|-----------------|  
|DisplayName|xs:string|アクティビティの表示名。|  
|状態|xs:string|補正の状態。|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName で返される文字列。|
