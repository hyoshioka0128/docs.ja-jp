---
title: "'<classname>' は継承元のインターフェイス '<interfacename>' が CLS に準拠していないため、CLS に準拠していません。"
ms.date: 07/20/2015
f1_keywords:
- bc40029
- vbc40029
helpviewer_keywords:
- BC40029
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
ms.openlocfilehash: 24a0866544cc3cd058672d18c6a7670b0b1bb489
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64584212"
---
# <a name="classname-is-not-cls-compliant-because-the-interface-interfacename-it-implements-is-not-cls-compliant"></a>'\<classname>' は継承元のインターフェイス '\<interfacename>' が CLS に準拠していないため、CLS に準拠していません
クラスまたはインターフェイスが `<CLSCompliant(True)>` としてマークされていますが、これらの派生元の型、またはこれらが実装している型が `<CLSCompliant(False)>` としてマークされているか、マークされていません。  
  
 クラスまたはインターフェイスを[言語への非依存性および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) に準拠させるには、その継承階層全体を準拠させる必要があります。 つまり、直接的または間接的に継承する型をすべて CLS に準拠させる必要があります。 同様に、クラスが 1 つ以上のインターフェイスを実装する場合は、そのすべてのインターフェイスの継承階層全体を CLS 準拠にする必要があります。  
  
 プログラミング要素に <xref:System.CLSCompliantAttribute> を適用する場合は、準拠または非準拠を示すために、属性の `isCompliant` パラメーターを `True` または `False` のどちらかに設定します。 このパラメーターには既定値がありません。値を指定する必要があります。  
  
 要素に <xref:System.CLSCompliantAttribute> を適用しないと、その要素は非準拠と見なされます。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40029  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- CLS 準拠にする必要がある場合は、この型を別の継承階層または実装スキームの中で定義します。  
  
- この型を現在の継承階層または実装スキームに残しておく必要がある場合は、 <xref:System.CLSCompliantAttribute> を定義から削除するか、 `<CLSCompliant(False)>`としてマークします。  
