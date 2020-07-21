---
title: 名前空間の名前
description: .NET ライブラリを拡張および操作するライブラリを設計するためのガイドラインの一部として名前空間の名前を付けるには、次のガイドラインに従います。
ms.date: 10/22/2008
helpviewer_keywords:
- names [.NET Framework], conflicts
- names [.NET Framework], namespaces
- type names, conflicts
- namespaces [.NET Framework], names
- names [.NET Framework], type names
ms.assetid: a49058d2-0276-43a7-9502-04adddf857b2
ms.openlocfilehash: e435e0281165b4a9f12bbccbeb10401b57375dcb
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290202"
---
# <a name="names-of-namespaces"></a>名前空間の名前
他の命名ガイドラインと同様に、名前空間に名前を付ける際の目的は、名前空間の内容がどのようなものである可能性があるかをすぐに把握するために、フレームワークを使用するプログラマにとって十分なわかりやすいものにすることです。 次のテンプレートは、名前空間の名前付けに関する一般的な規則を指定します。

 `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`

 次に例を示します。

 `Fabrikam.Math` `Litware.Security`

 異なる企業の名前空間が同じ名前にならないように、会社名を使用して名前空間名にプレフィックスを付ける✔️ます。

 名前空間名の2番目のレベルでは、バージョンに依存しない安定した製品名を使用✔️ます。

 ❌企業内のグループ名は有効期間が短くなる傾向があるため、名前空間階層内の名前の基準として組織階層を使用しないでください。 関連するテクノロジのグループを中心に、名前空間の階層を整理します。

 ✔️は、文字の大文字と小文字の区別を使用し、ピリオドを使用して名前空間コンポーネントを分離します (例: `Microsoft.Office.PowerPoint` )。 ブランドで nontraditional の大文字と小文字の区別が使用されている場合は、通常の名前空間の大文字と小文字が異なる場合でも、ブランドで定義されている大文字と小文字を

 ✔️、必要に応じて複数形の名前空間を使用することを検討してください。

 たとえば、`System.Collection` の代わりに `System.Collections` を使用します。 ただし、ブランド名と頭字語は、このルールの例外です。 たとえば、`System.IOs` の代わりに `System.IO` を使用します。

 ❌名前空間とその名前空間の型に同じ名前を使用しないでください。

 たとえば、名前空間名としてを使用せずに、 `Debug` `Debug` 同じ名前空間内にという名前のクラスを指定することはできません。 いくつかのコンパイラでは、このような型を完全に修飾する必要があります。

### <a name="namespaces-and-type-name-conflicts"></a>名前空間と型名の競合
 ❌、、、などのジェネリック型の名前は導入しないでください `Element` `Node` `Log` `Message` 。

 これを行うと、一般的なシナリオでの型名の競合が発生する可能性が非常に高くなります。 ジェネリック型名を修飾する必要があり `FormElement` ます (、、 `XmlNode` `EventLog` 、 `SoapMessage` )。

 名前空間のカテゴリごとに型名の競合を回避するための特定のガイドラインがあります。

- **アプリケーションモデルの名前空間**

     1つのアプリケーションモデルに属する名前空間は、一緒に使用されることがよくありますが、他のアプリケーションモデルの名前空間で使用されることはほとんどありません。 たとえば、名前空間は、 <xref:System.Windows.Forms?displayProperty=nameWithType> 名前空間と共に使用することはほとんど <xref:System.Web.UI?displayProperty=nameWithType> ありません。 既知のアプリケーションモデル名前空間グループの一覧を次に示します。

     `System.Windows*` `System.Web.UI*`

     ❌単一のアプリケーションモデル内の名前空間の型に同じ名前を付けないでください。

     たとえば、という名前の型を名前空間に追加しないでください。名前空間には、 `Page` <xref:System.Web.UI.Adapters?displayProperty=nameWithType> という名前の型が <xref:System.Web.UI?displayProperty=nameWithType> 既に含まれてい `Page` ます。

- **インフラストラクチャの名前空間**

     このグループには、一般的なアプリケーションの開発時にインポートされることがほとんどない名前空間が含まれています。 たとえば、 `.Design` 名前空間は主にプログラミングツールを開発するときに使用されます。 これらの名前空間の型との競合を回避することは、重要ではありません。

- **コア名前空間**

     コア名前空間には `System` 、アプリケーションモデルの名前空間とインフラストラクチャの名前空間を除く、すべての名前空間が含まれます。 コア名前空間には、他の、、、、およびが含ま `System` `System.IO` `System.Xml` `System.Net` れます。

     ❌コア名前空間の型と競合する型名を指定しないでください。

     たとえば、 `Stream` 型名としてを使用しないでください。 これは <xref:System.IO.Stream?displayProperty=nameWithType> 、よく使用される型と競合します。

- **テクノロジ名前空間グループ**

     このカテゴリには、やなど、同じ最初の2つの名前空間ノードを持つすべての名前空間が含まれ `(<Company>.<Technology>*` `Microsoft.Build.Utilities` `Microsoft.Build.Tasks` ます。 1つのテクノロジに属する型が互いに競合しないことが重要です。

     ❌1つのテクノロジ内の他の型と競合する型名を割り当てないでください。

     ❌テクノロジ名前空間の型とアプリケーションモデルの名前空間の間で型名の競合を発生させないでください (テクノロジがアプリケーションモデルで使用されることを想定していない場合)。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [名前付けのガイドライン](naming-guidelines.md)
