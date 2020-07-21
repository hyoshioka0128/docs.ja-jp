---
title: .NET Framework 型の文字列への変換
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: dc2e2b65-f623-4dc3-938b-d2a054d6832c
ms.openlocfilehash: d232fb0e3ea4cf3189294d6e6f43ae9270417407
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287819"
---
# <a name="converting-net-framework-types-to-strings"></a>.NET Framework 型の文字列への変換
.NET Framework 型を文字列に変換するには、**ToString** メソッドを使用します。 **ToString** メソッドは、渡された型の文字列表現を返します。 XML スキーマ (XSD) 仕様に対応する形式で文字列を返す .NET Framework 型を、次の表に示します。  
  
|.NET Framework 型|返される文字列型|  
|-------------------------|--------------------------|  
|ブール型|"true"、"false"|  
|Single.PositiveInfinity|"INF"|  
|Single.NegativeInfinity|"-INF"|  
|Double.PositiveInfinity|"INF"|  
|Double.NegativeInfinity|"-INF"|  
|DateTime|形式は、yyyy-MM-ddTHH:mm:sszzzzzz およびそのサブセットです。|  
|Timespan|PnYnMnTnHnMnS の形式。たとえば、`P2Y10M15DT10H30M20S` は 2 年 10 か月 15 日 10 時間 30 分 20 秒の期間です。|  
  
## <a name="see-also"></a>関連項目

- [XML データ型の変換](conversion-of-xml-data-types.md)
- [文字列の .NET Framework データ型への変換](converting-strings-to-dotnet-data-types.md)
