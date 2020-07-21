---
title: '方法: ジェネリック クラスを使用する'
ms.date: 07/20/2015
helpviewer_keywords:
- type parameters [Visual Basic], defining
- data type arguments [Visual Basic], defining
- arguments [Visual Basic], data types
- Of keyword [Visual Basic], using
- generic parameters
- data type parameters
- generics [Visual Basic], about generics
- data types [Visual Basic], as parameters
- data types [Visual Basic], as arguments
- parameters [Visual Basic], type
- types [Visual Basic], generic
- parameters [Visual Basic], generic
- generics [Visual Basic], creating generic types
- data type arguments
- parameters [Visual Basic], data type
- data type parameters [Visual Basic], defining
- type arguments [Visual Basic], defining
- arguments [Visual Basic], type
ms.assetid: 242dd2a6-86c4-4ce7-83f2-f2661803f752
ms.openlocfilehash: 01f1f7ef5963feeb3fe2b5390244e4e516773bad
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393845"
---
# <a name="how-to-use-a-generic-class-visual-basic"></a>方法: ジェネリック クラスを使用する (Visual Basic)
*型パラメーター* を受け取るクラスは、 *ジェネリック クラス*と呼ばれます。 ジェネリック クラスを使用している場合は、このパラメーターのそれぞれに *型引数* を入力することで、ジェネリック クラスから *構築済みクラス* を生成することができます。 これで、構築済みクラス型の変数を宣言し、構築済みクラスのインスタンスを作成して、その変数に割り当てることができます。  
  
 クラスに加えて、ジェネリックの構造体、インターフェイス、プロシージャ、デリゲートを定義して利用することもできます。  
  
 次のプロシージャは、.NET Framework で定義されたジェネリック クラスを受け取り、そこからインスタンスを作成します。  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a>型パラメーターを受け取るクラスを使用するには  
  
1. ソース ファイルの先頭に [Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) を含めて、<xref:System.Collections.Generic?displayProperty=nameWithType> 名前空間をインポートします。 これにより、<xref:System.Collections.Queue?displayProperty=nameWithType> などの他のキュー クラスと区別するために完全修飾しなくても <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> クラスを参照できるようになります。  
  
2. 通常の方法でオブジェクトを作成し、クラス名の直後に `(Of type)` を追加します。  
  
     次の例では、同じクラス (<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>) を使用して、異なるデータ型の項目を保持する 2 つのキュー オブジェクトを作成しています。 項目は各キューの末尾に追加された後に削除され、各キューの先頭から項目が表示されます。  
  
     [!code-vb[VbVbalrDataTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [Generic Types in Visual Basic](generic-types.md)
- [言語への非依存性、および言語非依存コンポーネント](../../../../standard/language-independence-and-language-independent-components.md)
- [Of](../../../language-reference/statements/of-clause.md)
- [Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [方法: 複数のデータ型に同一の機能を提供できるクラスを定義する](how-to-define-a-class-that-can-provide-identical-functionality.md)
- [反復子](../../concepts/iterators.md)
