---
title: <proceduresignature1> は、配列パラメーター型の配列または配列パラメーター型のランクのみが異なる <proceduresignature2> をオーバーロードするため、CLS に準拠していません。
ms.date: 07/20/2015
f1_keywords:
- vbc40035
- bc40035
helpviewer_keywords:
- BC40035
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
ms.openlocfilehash: 6143ebfbe7f131b0e196e531ed4282c8333be4ea
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250180"
---
# <a name="proceduresignature1-is-not-cls-compliant-because-it-overloads-proceduresignature2-which-differs-from-it-only-by-array-of-array-parameter-types-or-by-the-rank-of-the-array-parameter-types"></a>\<proceduresignature1> は、配列パラメーター型の配列または配列パラメーター型のランクのみが異なる \<proceduresignature2> をオーバーロードするため、CLS に準拠していません

プロシージャまたはプロパティが別のプロシージャまたはプロパティをオーバーライドする場合、そのプロシージャまたはプロパティは `<CLSCompliant(True)>` としてマークされます。それらのパラメーター リスト間の唯一の違いは、ジャグ配列または配列のランクの入れ子レベルです。
  
 次の宣言では、2 番目と 3 番目の宣言によってこのエラーが生成されます。
  
 `Overloads Sub ProcessArray(arrayParam() As Integer)`  
  
 `Overloads Sub ProcessArray(arrayParam()() As Integer)`  
  
 `Overloads Sub ProcessArray(arrayParam(,) As Integer)`  
  
 2 番目の宣言では、元の 1 次元パラメーター `arrayParam` を配列の配列に変更します。 3 番目の宣言は、`arrayParam` を 2 次元配列 (ランク 2) に変更します。 Visual Basic では、これらの変更のいずれかによってのみオーバーロードが異なることが許可されますが、そのようなオーバーロードは、[言語への非依存性、および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) に準拠していません。  
  
 プログラミング要素に <xref:System.CLSCompliantAttribute> を適用する場合は、属性の `isCompliant` パラメーターを `True` または `False` のどちらかに設定して、準拠または非準拠を示します。 このパラメーターには既定値がありません。値を指定する必要があります。  
  
 要素に <xref:System.CLSCompliantAttribute> を適用しないと、その要素は非準拠と見なされます。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40035  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- CLS 準拠が必要な場合は、このヘルプ ページで言及されている変更だけよりも多くの点で、相互に異なるようにオーバーロードを定義します。
- このヘルプ ページで言及されている変更によってのみオーバーロードが異なるようにする必要がある場合は、それらの定義から <xref:System.CLSCompliantAttribute> を削除するか、それらを `<CLSCompliant(False)>` とマークします。
  
## <a name="see-also"></a>関連項目

- [プロシージャのオーバーロード](../../programming-guide/language-features/procedures/procedure-overloading.md)
- [Overloads](../modifiers/overloads.md)
