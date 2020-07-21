---
title: MustInherit
ms.date: 07/20/2015
f1_keywords:
- MustInherit
- vb.MustInherit
helpviewer_keywords:
- classes [Visual Basic], abstract
- MustInherit classes [Visual Basic], MustInherit keyword
- abstract classes [Visual Basic], MustInherit class
- MustInherit keyword [Visual Basic]
ms.assetid: b8f05185-90e3-4dd7-adc2-90d852fab5b4
ms.openlocfilehash: 84df7a5cfdad3b5bc6764675725a5d0cb402b0b7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396208"
---
# <a name="mustinherit-visual-basic"></a>MustInherit (Visual Basic)
クラスが基底クラスとしてのみ使用でき、オブジェクトを直接作成できないことを示します。  
  
## <a name="remarks"></a>Remarks  
 *基底クラス* (*抽象クラス*とも呼ばれます) の目的は、このクラスから派生したすべてのクラスに共通の機能を定義することです。 これにより、派生クラスで共通の要素を再定義する必要がなくなります。 場合によっては、この共通機能は使用可能なオブジェクトを作成するのに十分ではなく、各派生クラスで不足している機能が定義されます。 このような場合は、使用しているコードで派生クラスからのみオブジェクトを作成する必要があります。 これを適用するには、基底クラスで `MustInherit` を使用します。  
  
 `MustInherit` クラスのもう 1 つの用途は、変数を関連するクラスのセットに制限することです。 基底クラスを定義し、そこから関連するすべてのクラスを派生させることができます。 基底クラスがすべての派生クラスに共通する機能を提供する必要はありませんが、変数に値を代入するためのフィルターとして使用できます。 使用しているコードが変数を基底クラスとして宣言している場合は、Visual Basic によって、派生クラスのいずれかからその変数にオブジェクトのみを割り当てることができます。  
  
 .NET Framework は、<xref:System.Array>、<xref:System.Enum>、<xref:System.ValueType> などのいくつかの `MustInherit` クラスを定義します。 <xref:System.ValueType> は、変数を制限する基底クラスの例です。 すべての値の型は <xref:System.ValueType> から派生します。 変数を <xref:System.ValueType> として宣言する場合は、その変数に値の型のみを割り当てることができます。  
  
## <a name="rules"></a>ルール  
  
- **宣言コンテキスト。** `Class` ステートメントでは `MustInherit` のみ使用できます。  
  
- **結合された修飾子。** 同じ宣言内で `MustInherit` を `NotInheritable` と共に指定することはできません。  
  
## <a name="example"></a>例  
 継承の強制とオーバーライドの強制の両方の例を次に示します。 基底クラス `shape` は `acrossLine` 変数を定義します。 クラス `circle` および `square` は `shape` から派生します。 これらは `acrossLine` の定義を継承しますが、その計算は図形の種類ごとに異なるため、関数 `area` を定義する必要があります。  
  
 [!code-vb[VbVbalrKeywords#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#2)]  
  
 `shape1` と `shape2` を型 `shape` として宣言できます。 ただし、`shape` からオブジェクトを作成することはできません。これには関数 `area` の機能がなく、`MustInherit` としてマークされているためです。  
  
 これらは `shape` として宣言されているため、変数 `shape1` および `shape2` は、派生クラス `circle` および `square` のオブジェクトに制限されます。 Visual Basic では、これらの変数に他のオブジェクトを割り当てることはできません。これにより、高いレベルのタイプ セーフが実現します。  
  
## <a name="usage"></a>使用方法  
 `MustInherit` 修飾子は、次のコンテキストで使用できます。  
  
 [Class ステートメント](../statements/class-statement.md)  
  
## <a name="see-also"></a>関連項目

- [Inherits ステートメント](../statements/inherits-statement.md)
- [NotInheritable](notinheritable.md)
- [キーワード](../keywords/index.md)
- [継承の基本](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
