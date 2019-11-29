---
title: パラメーターのデザイン
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines [.NET Framework], parameters
- members [.NET Framework], parameters
- names [.NET Framework], parameters
- parameters, design guidelines
- reserved parameters
ms.assetid: 3f33bf46-4a7b-43b3-bb78-1ffebe0dcfa6
author: KrzysztofCwalina
ms.openlocfilehash: 28b00f5911bb47536ec44b96f284e47b6c671149
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353746"
---
# <a name="parameter-design"></a>パラメーターのデザイン
このセクションでは、引数をチェックするためのガイドラインを含むセクションなど、パラメーターの設計に関する広範なガイドラインを示します。 また、「[パラメーターの名前付け](../../../docs/standard/design-guidelines/naming-parameters.md)」で説明されているガイドラインを参照してください。  
  
 **✓ DO** メンバーで必要な機能を提供する少なくとも派生パラメーター型を使用します。  
  
 たとえば、コレクションを列挙し、各項目をコンソールに出力するメソッドを設計するとします。 このようなメソッドは、<xref:System.Collections.ArrayList> または <xref:System.Collections.IList>ではなく、パラメーターとして <xref:System.Collections.IEnumerable> する必要があります。たとえば、のようになります。  
  
 **X DO NOT** 予約済みのパラメーターを使用します。  
  
 将来のバージョンでメンバーへの入力が増えると、新しいオーバーロードを追加できるようになります。  
  
 **X DO NOT** ポインター、ポインターの配列または多次元配列をパラメーターとして受け取るメソッドがパブリックに公開します。  
  
 ポインターと多次元配列は、適切に使用するのが比較的困難です。 ほとんどの場合、これらの型をパラメーターとして使用しないように、Api を再設計することができます。  
  
 **✓ DO** すべて配置`out`で値をすべてのパラメーターと`ref`パラメーター (除外パラメーター配列) のパラメーターの順序のオーバー ロード間の不整合が発生する場合でも (を参照してください[メンバーオーバー ロード](../../../docs/standard/design-guidelines/member-overloading.md))。  
  
 `out` パラメーターは、追加の戻り値として表示できます。また、これらをまとめてグループ化することで、メソッドのシグネチャがわかりやすくなります。  
  
 **✓ DO** メンバーをオーバーライドするときに名前のパラメーターまたはインターフェイス メンバーの実装で一貫しています。  
  
 これにより、メソッド間の関係がより適切に伝えられます。  
  
### <a name="choosing-between-enum-and-boolean-parameters"></a>列挙型パラメーターとブール型パラメーターの選択  
 **✓ DO** メンバーが 2 つ以上のブール型パラメーターを持っている場合は、列挙型を使用します。  
  
 **X DO NOT** ブール値を使用してない場合は、絶対に 3 つ以上の値が必要な表示できなくなります。  
  
 列挙型を使用すると、後で値を追加できるようになりますが、列挙型に値を追加することによるすべての影響に注意する必要があります。これについては、「 [Enum Design](../../../docs/standard/design-guidelines/enum.md)」を参照してください。  
  
 **✓ CONSIDER** は本当に 2 つの状態の値であり、のみを使用してブール型プロパティを初期化するコンス トラクターのパラメーターのブール値を使用します。  
  
### <a name="validating-arguments"></a>引数の検証  
 **✓ DO** パブリック、プロテクト、または明示的に実装されたメンバーに渡される引数を検証します。 検証が失敗した場合は、<xref:System.ArgumentException?displayProperty=nameWithType>、またはそのサブクラスの1つをスローします。  
  
 実際の検証は、必ずしもパブリックメンバーまたはプロテクトメンバーに対して行われる必要がないことに注意してください。 これは、一部のプライベートまたは内部ルーチンの下位レベルで発生する可能性があります。 主な点は、エンドユーザーに公開されているすべての領域が、引数をチェックすることです。  
  
 **✓ DO** スロー <xref:System.ArgumentNullException> null 引数が渡され、メンバーが null の引数をサポートしていない場合。  
  
 **✓ DO** 列挙型のパラメーターを検証します。  
  
 Enum 引数が列挙型によって定義された範囲内にあると仮定しないでください。 CLR では、列挙型で値が定義されていない場合でも、任意の整数値を列挙値にキャストできます。  
  
 **X DO NOT** 使用<xref:System.Enum.IsDefined%2A?displayProperty=nameWithType>enum の範囲を確認します。  
  
 **✓ DO** 変更可能な引数がありますが変更されている検証後に注意してください。  
  
 メンバーがセキュリティに依存している場合は、コピーを作成して、引数を検証して処理することをお勧めします。  
  
### <a name="parameter-passing"></a>パラメーターの引き渡し  
 フレームワークデザイナーの観点から見ると、パラメーターの主なグループには、値渡しパラメーター、`ref` パラメーター、`out` パラメーターの3つがあります。  
  
 値渡しのパラメーターを通じて引数が渡されると、メンバーは渡された実際の引数のコピーを受け取ります。 引数が値型の場合は、引数のコピーがスタックに格納されます。 引数が参照型の場合は、参照のコピーがスタックに配置されます。 C#、VB.NET、 C++など、最も一般的な CLR 言語は、既定で値渡しでパラメーターを渡します。  
  
 引数が `ref` パラメーターを通じて渡されると、メンバーは渡された実際の引数への参照を受け取ります。 引数が値型の場合は、引数への参照がスタックに格納されます。 引数が参照型の場合は、参照への参照がスタックに配置されます。 `Ref` パラメーターを使用して、呼び出し元によって渡される引数をメンバーが変更できるようにすることができます。  
  
 `Out` パラメーターは `ref` パラメーターに似ていますが、若干の違いがあります。 パラメーターは、最初は未割り当てと見なされ、何らかの値が割り当てられる前にメンバー本体で読み取ることはできません。 また、メンバーがを返す前に、パラメーターに何らかの値が割り当てられている必要があります。  
  
 **X AVOID** を使用して`out`または`ref`パラメーター。  
  
 `out` パラメーターまたは `ref` パラメーターを使用するには、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 また、`out` パラメーターと `ref` パラメーターの違いはあまり理解されていません。 一般ユーザー向けに設計されたフレームワーク設計者は、ユーザーが `out` または `ref` パラメーターをマスターに使用することを想定してはなりません。  
  
 **X DO NOT** 参照型を参照渡しされます。  
  
 ルールには、参照のスワップに使用できるメソッドなど、いくつかの例外があります。  
  
### <a name="members-with-variable-number-of-parameters"></a>パラメーターの数が可変のメンバー  
 可変個の引数を受け取ることができるメンバーは、配列パラメーターを指定することによって表現されます。 たとえば、<xref:System.String> には次のような方法があります。  
  
```csharp  
public class String {  
    public static string Format(string format, object[] parameters);  
}  
```  
  
 ユーザーは、次のように <xref:System.String.Format%2A?displayProperty=nameWithType> メソッドを呼び出すことができます。  
  
 `String.Format("File {0} not found in {1}",new object[]{filename,directory});`  
  
 C# Params キーワードを配列パラメーターに追加すると、パラメーターがいわゆる params array パラメーターに変更され、一時配列を作成するためのショートカットが提供されます。  
  
```csharp  
public class String {  
    public static string Format(string format, params object[] parameters);  
}  
```  
  
 これにより、ユーザーは配列要素を引数リストに直接渡すことによって、メソッドを呼び出すことができます。  
  
 `String.Format("File {0} not found in {1}",filename,directory);`  
  
 Params キーワードは、パラメーターリストの最後のパラメーターにのみ追加できることに注意してください。  
  
 **✓ CONSIDER** 要素の数が少ない配列を渡すエンドユーザーが予想される場合、配列パラメーターに、params キーワードを追加します。 多くの要素が共通のシナリオで渡されることが予想される場合、ユーザーはこれらの要素をインラインで渡すことはないため、params キーワードは必要ありません。  
  
 **X AVOID** があれば、呼び出し元はほとんどの場合、入力既に配列内に params 配列を使用します。  
  
 たとえば、バイト配列パラメーターを持つメンバーは、個々のバイトを渡すことで呼び出されることはほとんどありません。 このため、.NET Framework のバイト配列パラメーターでは、params キーワードは使用されません。  
  
 **X DO NOT** params 配列パラメーターを受け取るメンバーによって、配列が変更された場合、params 配列を使用します。  
  
 多くのコンパイラがメンバーの引数を呼び出しサイトの一時配列に変換するので、配列は一時オブジェクトである可能性があるため、配列に対する変更はすべて失われます。  
  
 **✓ CONSIDER** 単純なオーバー ロードで、params キーワードを使用する場合でもより複雑なオーバー ロードでは使用できませんでした。  
  
 ユーザーがすべてのオーバーロードに含まれていなくても、1つのオーバーロードで params 配列を持つことができるかどうかを確認してください。  
  
 **✓ DO** パラメーターを params キーワードを使用できるようにすることです。  
  
 **✓ CONSIDER** 非常にパフォーマンスが重視される Api の引数の数が少ない呼び出しに対して特別なオーバー ロードとコード パスを提供します。  
  
 これにより、API が少数の引数で呼び出された場合に、配列オブジェクトを作成しないようにすることができます。 配列パラメーターの単数形を取得し、数値のサフィックスを追加することによって、パラメーターの名前を形成します。  
  
 これは、単に配列を作成してより一般的なメソッドを呼び出すだけでなく、コードパス全体を特殊なケースにする場合にのみ実行してください。  
  
 **✓ DO** params 配列引数として null を渡すことがあります。  
  
 処理する前に、配列が null でないことを検証する必要があります。  
  
 **X DO NOT** を使用して、`varargs`メソッド、それ以外の場合、省略記号と呼ばれます。  
  
 などの一部の CLR 言語C++では、`varargs` メソッドと呼ばれる変数パラメーターリストを渡すための代替規則がサポートされています。 この規則は、CLS に準拠していないため、フレームワークでは使用しないでください。  
  
### <a name="pointer-parameters"></a>ポインター パラメーター  
 一般に、適切にデザインされたマネージコードフレームワークの公開領域にポインターを表示することはできません。 ほとんどの場合、ポインターはカプセル化する必要があります。 ただし、相互運用性の理由からポインターが必要になる場合もあれば、ポインターを使用することが適切な場合もあります。  
  
 **✓ DO** ポインターが CLS 準拠ではないために、ポインター引数を受け取り、メンバーの代替を提供します。  
  
 **X AVOID** 高い引数のポインター引数のチェックを実行します。  
  
 **✓ DO** 共通ポインターに関連する規則を伴うメンバーをデザインするときに従う必要です。  
  
 たとえば、単純なポインター演算を使用して同じ結果を得ることができるため、開始インデックスを渡す必要はありません。  
  
 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*  
  
 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*  
  
## <a name="see-also"></a>参照

- [メンバーのデザインのガイドライン](../../../docs/standard/design-guidelines/member.md)
- [フレームワーク デザインのガイドライン](../../../docs/standard/design-guidelines/index.md)
