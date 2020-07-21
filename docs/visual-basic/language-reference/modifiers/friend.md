---
title: Friend
ms.date: 07/20/2015
f1_keywords:
- vb.Friend
helpviewer_keywords:
- Friend keyword [Visual Basic]
- Friend access modifier
- Friend keyword [Visual Basic], syntax
- Protected Friend keyword combination
- Friend keyword [Visual Basic], and Protected
ms.assetid: b664605e-1c79-4728-b996-aa59c50846bc
ms.openlocfilehash: 4ac8e5942cf6097642ec111992ebfcdb91e8d7c1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392172"
---
# <a name="friend-visual-basic"></a>Friend (Visual Basic)
1 つ以上の宣言されたプログラミング要素が、その宣言を含むアセンブリ内からのみアクセス可能であることを示します。  
  
## <a name="remarks"></a>Remarks  
 多くの場合、クラスや構造体などのプログラミング要素は、それを宣言するコンポーネントだけでなく、アセンブリ全体で使用する必要があります。 ただし、アセンブリ外部のコードからアクセスできないようにすることもできます (アプリケーションが専用のものである場合など)。 この方法で要素へのアクセスを制限する場合は、`Friend` 修飾子を使用して宣言できます。  
  
 同じアセンブリにコンパイルされる他のクラス、構造体、およびモジュール内のコードは、そのアセンブリ内のすべての `Friend` 要素にアクセスできます。  
  
 `Friend` アクセスは、多くの場合はアプリケーションのプログラミング要素に優先されるレベルであり、`Friend` はインターフェイス、モジュール、クラス、または構造体の既定のアクセス レベルです。  
  
 `Friend` は、モジュール、インターフェイス、または名前空間レベルでのみ使用できます。 そのため、`Friend` 要素の宣言コンテキストはソース ファイル、名前空間、インターフェイス、モジュール、クラス、または構造体にする必要があり、プロシージャにすることはできません。  

> [!NOTE]
> また、[Protected Friend](protected-friend.md) アクセス修飾子を使用することもできます。これにより、クラス メンバーには、クラス内、派生クラス、およびクラスが定義されている同じアセンブリからアクセスできます。 クラス内および同じアセンブリ内の派生クラスからのメンバーへのアクセスを制限するには、[Private Protected](private-protected.md) アクセス修飾子を使用します。

 `Friend` とその他のアクセス修飾子の比較については、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
> [!NOTE]
> 別のアセンブリがフレンド アセンブリであることを指定できます。これにより、`Friend` としてマークされているすべての型とメンバーにアクセスできるようになります。 詳細については、[Friend アセンブリ](../../../standard/assembly/friend.md)に関するページを参照してください。

## <a name="example"></a>例  
 次のクラスは、`Friend` 修飾子を使用して、同じアセンブリ内の他のプログラミング要素が特定のメンバーにアクセスできるようにします。  
  
 [!code-vb[VbVbalrAccessModifiers#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalraccessmodifiers/vb/class1.vb#1)]  
  
## <a name="usage"></a>使用方法  
 `Friend` 修飾子は、次のコンテキストで使用できます。  
  
 [Class ステートメント](../statements/class-statement.md)  
  
 [Const ステートメント](../statements/const-statement.md)  
  
 [Declare ステートメント](../statements/declare-statement.md)  
  
 [Delegate ステートメント](../statements/delegate-statement.md)  
  
 [Dim ステートメント](../statements/dim-statement.md)  
  
 [Enum ステートメント](../statements/enum-statement.md)  
  
 [Event ステートメント](../statements/event-statement.md)  
  
 [Function ステートメント](../statements/function-statement.md)  
  
 [Interface ステートメント](../statements/interface-statement.md)  
  
 [Module ステートメント](../statements/module-statement.md)  
  
 [Property ステートメント](../statements/property-statement.md)  
  
 [Structure ステートメント](../statements/structure-statement.md)  
  
 [Sub ステートメント](../statements/sub-statement.md)  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [Public](public.md)
- [Protected](protected.md)
- [Private](private.md)
- [Private Protected](./private-protected.md)
- [Protected Friend](./protected-friend.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
