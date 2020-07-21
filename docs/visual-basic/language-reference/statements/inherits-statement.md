---
title: Inherits Statement
ms.date: 07/20/2015
f1_keywords:
- vb.Inherits
- Inherits
helpviewer_keywords:
- Inherits statement [Visual Basic]
- Inherits statement [Visual Basic], syntax
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
ms.openlocfilehash: 5d88a01f90bc91a88229d19aa2368f8c71075b2f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404500"
---
# <a name="inherits-statement"></a>Inherits Statement
現在のクラスまたはインターフェイスで、属性、変数、プロパティ、プロシージャ、およびイベントを別のクラスまたは一連のインターフェイスから継承させます。  
  
## <a name="syntax"></a>構文  
  
```vb  
Inherits basetypenames  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`basetypenames`|必須です。 このクラスの派生元のクラスの名前です。<br /><br /> \- または -<br /><br /> このインターフェイスの派生元のインターフェイスの名前です。 複数の名前を区切るには、コンマを使用します。|  
  
## <a name="remarks"></a>Remarks  
 使用した場合、`Inherits` ステートメントが、クラスまたはインターフェイス定義の最初の空行でもコメント行でもない行に記述されている必要があります。 それは、`Class` または `Interface` ステートメントの直後に追加する必要があります。  
  
 `Inherits` は、クラスまたはインターフェイスでのみ使用できます。 つまり、継承の宣言コンテキストは、ソース ファイル、名前空間、構造体、モジュール、プロシージャ、ブロックにすることができません。  
  
## <a name="rules"></a>ルール  
  
- **クラスの継承。** クラスで `Inherits` ステートメントを使用する場合、指定できる基底クラスは 1 つだけです。  
  
     クラスは、その中の入れ子にされたクラスから継承できません。  
  
- **インターフェイスの継承。** インターフェイスで `Inherits` ステートメントを使用している場合、1 つまたは複数の基底インターフェイスを指定できます。 それぞれが同じ名前のメンバーを定義している場合でも、2 つのインターフェイスから継承できます。 その場合、実装するコードでは、実装するメンバーを指定するために名前の修飾を使用する必要があります。  
  
     インターフェイスは、より制限の厳しいアクセス レベルの別のインターフェイスから継承することはできません。 たとえば、`Public` インターフェイスは、`Friend` インターフェイスから継承することはできません。  
  
     インターフェイスは、その中に入れ子にされたインターフェイスから継承することはできません。  
  
 .NET Framework でのクラス継承の例として、<xref:System.SystemException> クラスから継承する <xref:System.ArgumentException> クラスがあります。 これにより、<xref:System.ArgumentException> に、<xref:System.Exception.Message%2A> プロパティや <xref:System.Exception.ToString%2A> メソッドなど、システム例外に必要なすべての定義済みプロパティとプロシージャを提供できます。  
  
 .NET Framework でのインターフェイスの継承の例として、<xref:System.Collections.IEnumerable> インターフェイスから継承する <xref:System.Collections.ICollection> インターフェイスがあります。 これにより、<xref:System.Collections.ICollection> で、コレクションを走査するために必要な列挙子の定義が継承されます。  
  
## <a name="example"></a>例  
 次の例では、`Inherits` ステートメントを使用して、`thisClass` という名前のクラスで `anotherClass` という名前の基底クラスのすべてのメンバーを継承する方法を示しています。  
  
 [!code-vb[VbVbalrStatements#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#37)]  
  
## <a name="example"></a>例  
 次の例では、複数インターフェイスの継承を示しています。  
  
 [!code-vb[VbVbalrStatements#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#38)]  
  
 `thisInterface` という名前のインターフェイスに、<xref:System.IComparable>、<xref:System.IDisposable>、および <xref:System.IFormattable> インターフェイスのすべての定義が含まれるようになりました。継承されたメンバーではそれぞれ、2 つのオブジェクトの型固有の比較、割り当てられたリソースの解放、および `String` としてのオブジェクトの値の表現が提供されます。 `thisInterface` を実装するクラスでは、すべての基底インターフェイスのすべてのメンバーを実装する必要があります。  
  
## <a name="see-also"></a>関連項目

- [MustInherit](../modifiers/mustinherit.md)
- [NotInheritable](../modifiers/notinheritable.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
- [継承の基本](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [インターフェイス](../../programming-guide/language-features/interfaces/index.md)
