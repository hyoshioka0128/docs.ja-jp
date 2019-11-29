---
title: ポリモーフィズム - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, polymorphism
- polymorphism [C#]
ms.assetid: 086af969-29a5-4ce8-a993-0b7d53839dab
ms.openlocfilehash: be075c358d9ca2c36b6d173fca983c16f6b0d78c
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73970337"
---
# <a name="polymorphism-c-programming-guide"></a>ポリモーフィズム (C# プログラミング ガイド)
ポリモーフィズムは、カプセル化と継承に次ぐ、オブジェクト指向プログラミングの第 3 の柱と言われることがよくあります。 ポリモーフィズムは、ギリシャ語で "多形" を意味し、次の 2 つの側面を持っています。  
  
- メソッド パラメーター、コレクション、配列などに渡された派生クラスのオブジェクトは、実行時に基底クラスのオブジェクトとして扱われることがあります。 この場合、オブジェクトの宣言された型は、その実行時の型と同じではなくなります。  
  
- 基底クラスでは、[virtual](../../language-reference/keywords/virtual.md) *メソッド*を定義して実行できます。派生クラスでそれを[オーバーライド](../../language-reference/keywords/override.md)すると、独自の定義と実装を提供できます。 実行時には、クライアント コードがメソッドを呼び出したとき、CLR によってオブジェクトの実行時の型が検索され、仮想メソッドのオーバーライドが呼び出されます。 このように、ソース コード内で基底クラスのメソッドを呼び出して、派生クラスのメソッドが実行されるようにできます。  
  
 仮想メソッドを使用すると、関連するオブジェクトのグループを同一の方法で扱うことができます。 たとえば、描画サーフェイスにさまざまな種類の図形を作成できる描画アプリケーションがあるとします。 コンパイル時には、ユーザーがどのような種類の図形を作成するかわかりません。 しかし、アプリケーションでは、作成されたさまざまな種類の図形を追跡し、ユーザーのマウス操作に応じて更新する必要があります。 ポリモーフィズムを使用すると、2 つの基本的な手順でこの問題を解決できます。  
  
1. 各図形クラスが共通の基底クラスから派生するようなクラス階層を作成します。  
  
2. 仮想メソッドを使用して、基底クラスの 1 つのメソッドを呼び出すことで、派生クラスの適切なメソッドが呼び出されるようにします。  
  
 まず、`Shape` という基底クラスと、`Rectangle`、`Circle`、`Triangle` などの派生クラスを作成します。 `Shape` クラスで `Draw` という仮想メソッドを定義し、各派生クラスでそれをオーバーライドして、そのクラスが表す特定の図形を描画します。 `List<Shape>` オブジェクトを作成し、Circle、Triangle、および Rectangle を追加します。 描画サーフェイスを更新するには、[foreach](../../language-reference/keywords/foreach-in.md) ループを使用してリストを反復処理し、リスト内の各 `Shape` オブジェクトの `Draw` メソッドを呼び出します。 リスト内の各オブジェクトの宣言された型は `Shape` ですが、呼び出されるのは実行時の型 (それぞれの派生クラスでオーバーライドされたメソッド) になります。  
  
 [!code-csharp[csProgGuideInheritance#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#50)]  
  
 C# では、すべての型がポリモーフィックです。これは、ユーザー定義型を含むすべての型が <xref:System.Object> から派生するためです。  
  
## <a name="polymorphism-overview"></a>ポリモーフィズムの概要  
  
### <a name="virtual-members"></a>仮想メンバー  
 基底クラスから派生クラスを継承すると、派生クラスは、基底クラスのすべてのメソッド、フィールド、プロパティ、およびイベントを継承します。 派生クラスの設計者は、次の点を選択できます。  
  
- 基底クラスの仮想メンバーをオーバーライドするかどうか  
  
- 最も近い基底クラスのメソッドを、オーバーライドせずに継承するかどうか  
  
- これらのメンバーの仮想でない実装を新しく定義して、基底クラスの実装を隠ぺいするかどうか  
  
 派生クラスが基底クラスのメンバーをオーバーライドできるのは、基底クラスのメンバーが [virtual](../../language-reference/keywords/virtual.md) または [abstract](../../language-reference/keywords/abstract.md) として宣言されている場合だけです。 派生メンバーでは、[override](../../language-reference/keywords/override.md) キーワードを使用して、そのメソッドが仮想呼び出しに加わることを明示的に示す必要があります。 次にコード例を示します。  
  
 [!code-csharp[csProgGuideInheritance#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#20)]  
  
 フィールドは仮想メンバーにできません。仮想メンバーにできるのは、メソッド、プロパティ、イベント、およびインデクサーに限られます。 派生クラスが仮想メンバーをオーバーライドすると、派生クラスのメンバーは、そのクラスのインスタンスが基底クラスのインスタンスとしてアクセスされるときでも呼び出されます。 次にコード例を示します。  
  
 [!code-csharp[csProgGuideInheritance#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#21)]  
  
 仮想メソッドとプロパティを使用すると、派生クラスは、基底クラスのメソッドの実装を使用せずに基底クラスを拡張できます。 詳細については、「[Override キーワードと New キーワードによるバージョン管理](./versioning-with-the-override-and-new-keywords.md)」を参照してください。 1 つまたは一連のメソッドを定義し、その実装を派生クラスに任せるもう 1 つの方法として、インターフェイスがあります。 詳細については、「[インターフェイス](../interfaces/index.md)」を参照してください。  
  
### <a name="hiding-base-class-members-with-new-members"></a>新しいメンバーによる基底クラスのメンバーの隠ぺい  
 派生メンバーに基底クラスのメンバーと同じ名前を付けながら、そのメンバーが仮想呼び出しに加わらないようにするには、[new](../../language-reference/keywords/new-modifier.md) キーワードを使用します。 `new` キーワードは、置き換えられるクラス メンバーの戻り値の型の前に配置します。 次にコード例を示します。  
  
 [!code-csharp[csProgGuideInheritance#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#18)]  
  
 基底クラスのメンバーが隠ぺいされても、派生クラスのインスタンスを基底クラスのインスタンスにキャストすることで、クライアント コードから基底クラスのメンバーにアクセスできます。 次に例を示します。  
  
 [!code-csharp[csProgGuideInheritance#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#19)]  
  
### <a name="preventing-derived-classes-from-overriding-virtual-members"></a>派生クラスが仮想メンバーをオーバーライドしないようにする  
 仮想メンバーは、それを最初に宣言したクラスとの間でどれほど多くのクラスが宣言されても、いつまでも仮想のままです。 たとえば、クラス A が仮想メンバーを宣言し、クラス B がクラス A から派生し、クラス C がクラス B から派生した場合、クラス C は仮想メンバーを継承し、クラス B がその仮想メンバーのオーバーライドを宣言したかどうかに関係なく、そのメンバーをオーバーライドできます。 次にコード例を示します。  
  
 [!code-csharp[csProgGuideInheritance#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#22)]  
  
 派生クラスでは、オーバーライドを [sealed](../../language-reference/keywords/sealed.md) として宣言することで仮想継承を中止できます。 この場合、クラス メンバーの宣言で、`sealed` キーワードの前に `override` キーワードを指定する必要があります。 次にコード例を示します。  
  
 [!code-csharp[csProgGuideInheritance#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#24)]  
  
 上の例では、`DoWork` メソッドは C から派生したどのクラスに対しても仮想メソッドではありません。C のインスタンスに対しては、B 型や A 型にキャストされた場合でも、依然として仮想メソッドです。シール メソッドは、次のコード例に示すように、`new` キーワードを使用して派生クラスに置き換えることができます。  
  
 [!code-csharp[csProgGuideInheritance#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#25)]  
  
 このコード例では、`DoWork` が、D 型の変数を使用して D で呼び出されると、新しい `DoWork` が呼び出されます。 また、C 型、B 型、または A 型の変数を使用して D のインスタンスにアクセスした場合、`DoWork` への呼び出しは、仮想継承の規則に従って、クラス C の `DoWork` の実装に転送されます。  
  
### <a name="accessing-base-class-virtual-members-from-derived-classes"></a>派生クラスからの基底クラスの仮想メンバーへのアクセス  
 メソッドやプロパティを置き換えたり、オーバーライドしたりした派生クラスでは、`base` キーワードを使用して、基底クラスのメソッドやプロパティに引き続きアクセスできます。 次にコード例を示します。  
  
 [!code-csharp[csProgGuideInheritance#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#26)]  
  
 詳細については、「[base](../../language-reference/keywords/base.md)」を参照してください。  
  
> [!NOTE]
> 仮想メンバーの場合、その固有の実装で `base` を使用して、その仮想メンバーの基底クラス実装を呼び出すことをお勧めします。 基底クラスの動作を実行できるようにすることで、派生クラスは、派生クラスに固有の動作を実装することに集中できます。 基底クラス実装を呼び出さない場合は、基底クラスの動作と互換性のある動作を派生クラスで実現する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
- [Override キーワードと New キーワードによるバージョン管理](./versioning-with-the-override-and-new-keywords.md)  
  
- [Override キーワードと New キーワードを使用する場合について](./knowing-when-to-use-override-and-new-keywords.md)  
  
- [ToString メソッドをオーバーライドする方法](./how-to-override-the-tostring-method.md)
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [継承](./inheritance.md)
- [抽象クラスとシール クラス、およびクラス メンバー](./abstract-and-sealed-classes-and-class-members.md)
- [メソッド](./methods.md)
- [イベント](../events/index.md)
- [プロパティ](./properties.md)
- [インデクサー](../indexers/index.md)
- [型](../types/index.md)
