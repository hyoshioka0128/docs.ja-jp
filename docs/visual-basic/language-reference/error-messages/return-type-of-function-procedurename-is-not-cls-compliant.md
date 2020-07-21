---
title: 関数 '<procedurename>' の戻り値の型は CLS に準拠していません。
ms.date: 07/20/2015
f1_keywords:
- bc40027
- vbc40027
helpviewer_keywords:
- BC40027
ms.assetid: 33c088c7-48e7-400c-920e-6d8967e1f3fc
ms.openlocfilehash: 9cc7e25ef1be21ff2f6a71dcb61bc29ec92da30f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400358"
---
# <a name="return-type-of-function-procedurename-is-not-cls-compliant"></a>関数 '\<procedurename>' の戻り値の型は CLS に準拠していません。
`Function` プロシージャが `<CLSCompliant(True)>` としてマークされていますが、`<CLSCompliant(False)>` としてマークされている型、マークされていない型、または非準拠の型であるために修飾されていない型を返します。  
  
 プロシージャを[言語への非依存性および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) に準拠させるには、CLS 準拠型のみを使用する必要があります。 これは、パラメーターの型、戻り値の型、およびすべてのローカル変数の型に適用されます。  
  
 次の Visual Basic データ型は CLS に準拠していません。  
  
- [SByte データ型](../data-types/sbyte-data-type.md)  
  
- [UInteger データ型](../data-types/uinteger-data-type.md)  
  
- [ULong データ型](../data-types/ulong-data-type.md)  
  
- [UShort データ型](../data-types/ushort-data-type.md)  
  
 プログラミング要素に <xref:System.CLSCompliantAttribute> を適用する場合は、属性の `isCompliant` パラメーターを `True` または `False` のどちらかに設定して、準拠または非準拠を示します。 このパラメーターには既定値がありません。値を指定する必要があります。  
  
 要素に <xref:System.CLSCompliantAttribute> を適用しないと、その要素は非準拠と見なされます。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40027  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `Function` プロシージャがこの特定の型を返す必要がある場合は、<xref:System.CLSCompliantAttribute> を削除します。 プロシージャは CLS 準拠になりません。  
  
- `Function` プロシージャを CLS 準拠にする必要がある場合は、戻り値の型を最も近い CLS 準拠型に変更します。 たとえば、2,147,483,647 を超える値の範囲が不要な場合は、 `UInteger` の代わりに `Integer` を使用できます。 拡張範囲が必要な場合は、 `UInteger` の代わりに `Long`を使用できます。  
  
- オートメーション オブジェクトや COM オブジェクトとやり取りする場合は、一部の型のデータ幅が .NET Framework とは異なることに注意してください。 たとえば、他の多くの環境では `int` は 16 ビットです。 このようなコンポーネントに 16 ビット整数を返す場合、Visual Basic のマネージド コードでは、`Integer` ではなく `Short` を宣言してください。
