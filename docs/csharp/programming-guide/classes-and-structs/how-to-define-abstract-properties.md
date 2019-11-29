---
title: 抽象プロパティを定義する方法 - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
ms.openlocfilehash: 1b6dc1dfe932ffff161b0eef667bd35a75b66cf9
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73970998"
---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a>抽象プロパティを定義する方法 (C# プログラミング ガイド)
次の例では、[抽象](../../language-reference/keywords/abstract.md)プロパティを定義する方法を示します。 抽象プロパティの宣言では、プロパティ アクセサーは実装されません。クラスがプロパティをサポートしていることは宣言しますが、アクセサーの実装は派生クラスに委ねます。 基本クラスから継承された抽象プロパティを実装する方法を次の例に示します。  
  
 このサンプルは 3 つのファイルで構成され、それぞれ個別にコンパイルされ、生成されたアセンブリが次のコンパイルで参照されます。  
  
- abstractshape.cs: 抽象 `Shape` プロパティを含む `Area` クラス。  
  
- shapes.cs:`Shape` クラスのサブクラス。  
  
- shapetest.cs:`Shape` から派生したいくつかのオブジェクトの面積を表示するテスト プログラム。  
  
 この例をコンパイルするには、次のコマンドを使用します。  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 これで、実行可能ファイル shapetest.exe が作成されます。  
  
## <a name="example"></a>例  
 このファイルは、`double` 型の `Shape` プロパティを含む `Area` クラスを宣言します。  
  
 [!code-csharp[csProgGuideInheritance#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#1)]  
  
- プロパティの修飾子は、プロパティ宣言自体に設定されます。 次に例を示します。  
  
    ```csharp  
    public abstract double Area  
    ```  
  
- 抽象プロパティ (この例では `Area` など) を宣言する場合は、使用可能なアクセサーを示すだけで、実装はしません。 この例では、[get](../../language-reference/keywords/get.md) アクセサーのみが使用可能であるため、プロパティは読み取り専用となります。  
  
## <a name="example"></a>例  
 次のコードは、`Shape` の 3 つのサブクラスと、それらがどのように `Area` プロパティをオーバーライドして独自の実装を提供するかを示しています。  
  
 [!code-csharp[csProgGuideInheritance#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#2)]  
  
## <a name="example"></a>例  
 次のコードは、`Shape` から派生するオブジェクトをいくつか作成し、それらの面積を出力するテスト プログラムを示しています。  
  
 [!code-csharp[csProgGuideInheritance#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#3)]  
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [クラスと構造体](./index.md)
- [抽象クラスとシール クラス、およびクラス メンバー](./abstract-and-sealed-classes-and-class-members.md)
- [プロパティ](./properties.md)
