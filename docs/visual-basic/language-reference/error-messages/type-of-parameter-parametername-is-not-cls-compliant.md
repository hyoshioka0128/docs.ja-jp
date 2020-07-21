---
title: パラメーター '<parametername>' の型は CLS に準拠していません。
ms.date: 07/20/2015
f1_keywords:
- vbc40028
- bc40028
helpviewer_keywords:
- BC40028
ms.assetid: dfa1f6f9-bb88-44ad-b85f-149144363d41
ms.openlocfilehash: edbcadf271c4ccafc11e5b64eb103a0290976179
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413015"
---
# <a name="type-of-parameter-parametername-is-not-cls-compliant"></a>パラメーター '\<parametername>' の型は CLS に準拠していません。
プロシージャが `<CLSCompliant(True)>` としてマークされていますが、`<CLSCompliant(False)>` としてマークされている型、マークされていない型、または非準拠の型であるために修飾されていない型を持つパラメーターを宣言しています。  
  
 プロシージャを[言語への非依存性および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) に準拠させるには、CLS 準拠型のみを使用する必要があります。 これは、パラメーターの型、戻り値の型、およびすべてのローカル変数の型に適用されます。  
  
 次の Visual Basic データ型は CLS に準拠していません。  
  
- [SByte データ型](../data-types/sbyte-data-type.md)  
  
- [UInteger データ型](../data-types/uinteger-data-type.md)  
  
- [ULong データ型](../data-types/ulong-data-type.md)  
  
- [UShort データ型](../data-types/ushort-data-type.md)  
  
 プログラミング要素に <xref:System.CLSCompliantAttribute> を適用する場合は、属性の `isCompliant` パラメーターを `True` または `False` のどちらかに設定して、準拠または非準拠を示します。 このパラメーターには既定値がありません。値を指定する必要があります。  
  
 要素に <xref:System.CLSCompliantAttribute> を適用しないと、その要素は非準拠と見なされます。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40028  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- プロシージャがこの特定の型のパラメーターを受け取る必要がある場合は、<xref:System.CLSCompliantAttribute> を削除します。 プロシージャは CLS 準拠になりません。  
  
- プロシージャを CLS 準拠にする必要がある場合は、このパラメーターの型を、最も近い CLS 準拠型に変更します。 たとえば、2,147,483,647 を超える値の範囲が不要な場合は、 `UInteger` の代わりに `Integer` を使用できます。 拡張範囲が必要な場合は、 `UInteger` の代わりに `Long`を使用できます。  
  
- オートメーション オブジェクトや COM オブジェクトとやり取りする場合は、一部の型のデータ幅が .NET Framework とは異なることに注意してください。 たとえば、他の多くの環境では `int` は 16 ビットです。 このようなコンポーネントから 16 ビット整数を受け取る場合、Visual Basic のマネージド コードでは、`Integer` ではなく `Short` を宣言してください。
