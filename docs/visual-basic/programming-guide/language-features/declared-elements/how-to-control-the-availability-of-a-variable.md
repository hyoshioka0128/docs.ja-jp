---
title: '方法: 変数の可用性を制御する'
ms.date: 07/20/2015
helpviewer_keywords:
- access levels, declared elements
- Private keyword [Visual Basic], accessing variables
- access levels, variables
- Public keyword [Visual Basic], accessing variables
- Friend keyword [Visual Basic], accessing variables
- variables [Visual Basic], access level
- declared elements [Visual Basic], access level
- Protected keyword [Visual Basic], accessing variables
ms.assetid: eaf4f073-7922-43ce-ae1e-90ff376ae947
ms.openlocfilehash: 0bfa7fa2bdac4746827884c1dad62734c549a48e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357388"
---
# <a name="how-to-control-the-availability-of-a-variable-visual-basic"></a>方法: 変数の可用性を制御する (Visual Basic)
変数の可用性を制御するには、その*アクセス レベル*を指定します。 アクセス レベルによって、変数への読み取りまたは書き込みのアクセス許可を持つコードが決まります。  
  
- *メンバー変数* (モジュール レベルのプロシージャの外部で定義される) は、既定でパブリック アクセスになります。これは、それらを参照できるすべてのコードで、それらにアクセスできることを意味します。 これを変更するには、アクセス修飾子を指定します。  
  
- *ローカル変数* (プロシージャ内に定義) は、名目上パブリック アクセス権を持ちますが、それらのプロシージャ内のコードだけがそれらにアクセスできます。 ローカル変数のアクセス レベルを変更することはできませんが、それを含むプロシージャのアクセス レベルを変更することはできます。  
  
 詳しくは、「[Visual Basic でのアクセス レベル](access-levels.md)」を参照してください。  
  
## <a name="private-and-public-access"></a>プライベート アクセスとパブリック アクセス  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-module-class-or-structure"></a>変数をそのモジュール、クラス、または構造体内からのみアクセスできるようにするには  
  
1. モジュール、クラス、または構造体の内部で、ただしプロシージャの外部に、変数の [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を配置します。  
  
2. `Dim` ステートメントに [Private](../../../language-reference/modifiers/private.md) キーワードを含めます。  
  
     変数の読み取りや書き込みは、モジュール、クラス、または構造体内のどこからでも行うことができますが、その外部から行うことはできません。  
  
#### <a name="to-make-a-variable-accessible-from-any-code-that-can-see-it"></a>変数を参照できるすべてのコードから変数にアクセスできるようにするには  
  
1. メンバー変数の場合、変数の `Dim` ステートメントをモジュール、クラス、または構造体の内部で、ただしプロシージャの外部に配置します。  
  
2. `Dim` ステートメントに [Public](../../../language-reference/modifiers/public.md) キーワードを含めます。  
  
     アセンブリと相互運用するすべてのコードから変数の読み取りや書き込みができます。  
  
 \- または -  
  
1. ローカル変数の場合は、プロシージャ内に変数の `Dim` ステートメントを配置します。  
  
2. `Dim` ステートメントには `Public` キーワードを含めないでください。  
  
     変数の読み取りや書き込みは、プロシージャ内のどこからでも行うことができますが、その外部から行うことはできません。  
  
## <a name="protected-and-friend-access"></a>Protected アクセスと Friend アクセス  
 変数のアクセス レベルは、そのクラス、任意の派生クラス、またはそのアセンブリに制限できます。 また、これらの制限の和集合を指定することもできます。これにより、任意の派生クラスまたは同じアセンブリ内の他の任意の場所のコードからアクセスできるようになります。 この和集合を指定するには、同じ宣言で `Protected` キーワードと `Friend` キーワードを組み合わせます。  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-class-and-any-derived-classes"></a>そのクラスと任意の派生クラス内からのみ変数にアクセスできるようにするには  
  
1. 変数の `Dim` ステートメントをクラス内、ただしプロシージャの外部に配置します。  
  
2. `Dim` ステートメントに [Protected](../../../language-reference/modifiers/protected.md) キーワードを含めます。  
  
     変数の読み取りや書き込みは、クラス内のどこからでも、また、それから派生した任意のクラス内から行うことができますが、派生チェーン内のクラスの外部から行うことはできません。  
  
#### <a name="to-make-a-variable-accessible-only-from-within-the-same-assembly"></a>同じアセンブリ内からのみ変数にアクセスできるようにするには  
  
1. モジュール、クラス、または構造体の内部で、ただしプロシージャの外部に、変数の `Dim` ステートメントを配置します。  
  
2. `Dim` ステートメントに [Friend](../../../language-reference/modifiers/friend.md) キーワードを含めます。  
  
     変数の読み取りや書き込みは、モジュール、クラス、または構造体内のどこからでも、また同じアセンブリ内の任意のコードから行うことができますが、アセンブリの外部から行うことはできません。  
  
## <a name="example"></a>例  
 次の例は、`Public`、`Protected`、`Friend`、`Protected Friend`、および `Private` アクセス レベルによる変数の宣言を示しています。 `Dim` ステートメントでアクセス レベルを指定する場合は、`Dim` キーワードを含める必要はありません。  
  
```vb  
Public Class classForEverybody  
Protected Class classForMyHeirs  
Friend stringForThisProject As String  
Protected Friend stringForProjectAndHeirs As String  
Private numberForMeOnly As Integer  
```  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 変数のアクセス レベルの制限を強めるほど、悪意のあるコードによってそれが不正使用される可能性が低くなります。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic でのアクセス レベル](access-levels.md)
- [Dim ステートメント](../../../language-reference/statements/dim-statement.md)
- [Public](../../../language-reference/modifiers/public.md)
- [Protected](../../../language-reference/modifiers/protected.md)
- [Friend](../../../language-reference/modifiers/friend.md)
- [Private](../../../language-reference/modifiers/private.md)
