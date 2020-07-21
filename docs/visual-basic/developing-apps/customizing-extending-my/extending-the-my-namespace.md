---
title: My 名前空間の拡張
ms.date: 07/20/2015
f1_keywords:
- vb.AddingMyExtensions
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
- My namespace [Visual Basic], extending
ms.assetid: 808e8617-b01c-4135-8b21-babe87389e8e
ms.openlocfilehash: 2a7b0b84061fccd9a333a68e4a19477bd19ca4ff
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74330310"
---
# <a name="extending-the-my-namespace-in-visual-basic"></a>Visual Basic における `My` 名前空間の拡張

Visual Basic の `My` 名前空間は、.NET Framework の機能を簡単に活用できるようにするプロパティとメソッドを公開します。 `My` 名前空間により、一般的なプログラミングの問題が単純化されるため、多くの場合、難しいタスクを 1 行のコードに減らすことができます。 さらに、`My` 名前空間は完全に拡張可能であるため、`My` の動作をカスタマイズし、その階層に新しいサービスを追加して、特定のアプリケーションのニーズに適合させることができます。 このトピックでは、`My` 名前空間の既存のメンバーをカスタマイズする方法と、独自のカスタム クラスを `My` 名前空間に追加する方法について説明します。

## <a name="customizing-existing-my-namespace-members"></a>既存の `My` 名前空間のメンバーのカスタマイズ

Visual Basic の `My` 名前空間は、アプリケーションやコンピューターなどに関してよく使用される情報を公開します。 `My` 名前空間内のオブジェクトの完全な一覧については、「[My の参照](../../language-reference/keywords/my-reference.md)」を参照してください。 `My` 名前空間の既存のメンバーは、アプリケーションのニーズに合うようにカスタマイズすることが必要になる場合があります。 読み取り専用ではない、`My` 名前空間内のオブジェクトのすべてのプロパティは、カスタム値に設定できます。

たとえば、アプリケーションを実行しているユーザーの現在のセキュリティ コンテキストにアクセスするために、`My.User` オブジェクトを頻繁に使用するとします。 ただし、会社ではカスタムのユーザー オブジェクトを使用して、会社内のユーザーに追加の情報と機能を公開しています。 このシナリオでは、次の例に示すように、`My.User.CurrentPrincipal` プロパティの既定値を独自のカスタム プリンシパル オブジェクトのインスタンスに置き換えることができます。

[!code-vb[VbVbcnExtendingMy#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#1)]

`My.User` オブジェクトに `CurrentPrincipal` プロパティを設定すると、アプリケーションの実行に使用する ID が変更されます。 次に、`My.User` オブジェクトは、新たに指定されたユーザーに関する情報を返します。
  
## <a name="adding-members-to-my-objects"></a>`My` オブジェクトへのメンバーの追加

`My.Application` および `My.Computer` から返される型は `Partial` クラスとして定義されます。 そのため、`MyApplication` または `MyComputer` という名前の `Partial` クラスを作成することによって、`My.Application` および `My.Computer` オブジェクトを拡張できます。 このクラスを `Private` クラスにすることはできません。 クラスを `My` 名前空間の一部として指定した場合は、`My.Application` オブジェクトまたは `My.Computer` オブジェクトに含まれるプロパティおよびメソッドを追加できます。

次の例では、`DnsServerIPAddresses` という名前のプロパティを `My.Computer` オブジェクトに追加します。

[!code-vb[VbVbcnExtendingMy#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class2.vb#2)]

## <a name="adding-custom-objects-to-the-my-namespace"></a>`My` 名前空間へのカスタム オブジェクトの追加

`My` 名前空間には、多くの一般的なプログラミング タスクのためのソリューションが用意されていますが、`My` 名前空間が対応していないタスクが発生する場合があります。 たとえば、アプリケーションがユーザー データのカスタム ディレクトリ サービスにアクセスする場合や、アプリケーションが既定で Visual Basic にインストールされていないアセンブリを使用する場合があります。 `My` 名前空間を拡張して、環境に固有の一般的なタスクにカスタム ソリューションを含めることができます。 `My` 名前空間は、増え続けるアプリケーションのニーズに合わせて新しいメンバーを追加するために簡単に拡張できます。 また、Visual Basic テンプレートとして、`My` 名前空間の拡張機能を他の開発者に配置することもできます。
  
### <a name="adding-members-to-the-my-namespace"></a>`My` 名前空間へのメンバーの追加

`My` は他の名前空間と同じ名前空間であるため、モジュールを追加して `My` の `Namespace` を指定するだけで、最上位レベルのプロパティを追加できます。 次の例に示すように、`HideModuleName` 属性を使用してモジュールに注釈を設定します。 `HideModuleName` 属性を指定すると、`My` 名前空間のメンバーを表示するときに、IntelliSense によってモジュール名が表示されなくなります。

[!code-vb[VbVbcnExtendingMy#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#3)]

`My` 名前空間にメンバーを追加するには、必要に応じてモジュールにプロパティを追加します。 `My` 名前空間に追加したプロパティごとに、型 `ThreadSafeObjectProvider(Of T)` のプライベート フィールドを追加します。ここで、型はカスタム プロパティによって返される型です。 このフィールドは、`GetInstance` メソッドを呼び出すことでプロパティによって返されるスレッドセーフなオブジェクト インスタンスを作成するために使用されます。 その結果、拡張プロパティにアクセスする各スレッドは、返された型の独自のインスタンスを受け取ります。 次の例では、型 `SampleExtension` の `SampleExtension` という名前のプロパティを `My` 名前空間に追加します。

[!code-vb[VbVbcnExtendingMy#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#4)]

## <a name="adding-events-to-custom-my-objects"></a>カスタムの `My` オブジェクトへのイベントの追加

`My.Application` オブジェクトを使用して、`My` 名前空間の `MyApplication` 部分クラスを拡張することによって、カスタムの `My` オブジェクトのイベントを公開できます。 Windows ベースのプロジェクトの場合、**ソリューション エクスプローラー**でプロジェクトの **[マイ プロジェクト]** ノードをダブルクリックできます。 Visual Basic の**プロジェクト デザイナー**で、 **[アプリケーション]** タブをクリックし、 **[アプリケーション イベントの表示]** ボタンをクリックします。 *ApplicationEvents.vb* という名前の新しいファイルが作成されます。 これには、`MyApplication` クラスを拡張するための次のコードが含まれています。

[!code-vb[VbVbcnExtendingMy#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#5)]

カスタムの `My` オブジェクトのイベント ハンドラーは、`MyApplication` クラスにカスタム イベント ハンドラーを追加することで追加できます。 カスタム イベントを使用すると、イベント ハンドラーを追加または削除したりイベントが発生したりしたときに実行されるコードを追加できます。 カスタム イベントの `AddHandler` コードは、ユーザーがイベントを処理するためにコードを追加した場合にのみ実行されることに注意してください。 たとえば、前のセクションの `SampleExtension` オブジェクトに、カスタム イベント ハンドラーを追加したい `Load` イベントがあるとします。 次のコード例は、`My.SampleExtension.Load` イベントが発生したときに呼び出される `SampleExtensionLoad` という名前のカスタム イベント ハンドラーを示します。 新しい `My.SampleExtensionLoad` イベントを処理するコードを追加すると、このカスタム イベント コードの `AddHandler` の部分が実行されます。 `MyApplication_SampleExtensionLoad` メソッドは、`My.SampleExtensionLoad` イベントを処理するイベント ハンドラーの例を示すために、コード例に含まれています。 `SampleExtensionLoad` イベントは、*ApplicationEvents.vb* ファイルを編集しているときに、コード エディターの上にある左側のドロップダウン リストで **[My Application Events] (マイ アプリケーション イベント)** オプションを選択したときに使用できます。

[!code-vb[VbVbcnExtendingMy#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#6)]

## <a name="design-guidelines"></a>デザインのガイドライン

`My` 名前空間の拡張機能を開発するときは、次のガイドラインに従って、拡張コンポーネントのメンテナンス コストを最小限に抑えることができます。

- **拡張ロジックのみを含めます。** `My` 名前空間の拡張機能に含まれるロジックには、`My` 名前空間で必要な機能を公開するために必要なコードのみを含める必要があります。 拡張機能は、ユーザー プロジェクト内にソース コードとして存在し、拡張機能コンポーネントを更新するとメンテナンス コストが高くなるため、可能な場合は回避する必要があります。
- **プロジェクトの前提を最小限に抑えます。** `My` 名前空間の拡張機能を作成する場合は、一連の参照、プロジェクトレベルのインポート、または特定のコンパイラ設定 (たとえば、`Option Strict` オフ) を前提としないでください。 代わりに、`Global` キーワードを使用して、依存関係を最小限に抑え、すべての型参照を完全修飾してください。 また、拡張機能のエラーを最小限に抑えるために、拡張機能が `Option Strict` オンでコンパイルされるようにしてください。
- **拡張機能のコードを分離します。** コードを 1 つのファイルに配置すると、拡張機能を Visual Studio 項目テンプレートとして簡単に配置できるようになります。 詳細については、このトピックの後半の「拡張機能のパッケージ化と配置」を参照してください。 すべての `My` 名前空間拡張コードを 1 つのファイルまたはプロジェクト内の別のフォルダーに配置すると、ユーザーが `My` 名前空間の拡張機能を見つけることができます。

## <a name="designing-class-libraries-for-my"></a>`My` のクラス ライブラリの設計

ほとんどのオブジェクト モデルの場合と同様に、設計パターンの中には `My` 名前空間で適切に機能するものもあれば、そうでないものもあります。 `My` 名前空間の拡張機能を設計するときは、次の原則を考慮してください。

- **ステートレス メソッド。** `My` 名前空間のメソッドは、特定のタスクに完全なソリューションを提供する必要があります。 メソッドに渡されたパラメーター値が、特定のタスクを完了するために必要なすべての入力を提供していることを確認してください。 リソースへのオープン接続など、以前の状態に依存するメソッドを作成しないようにしてください。
- **グローバル インスタンス。** `My` 名前空間で保持される唯一の状態は、プロジェクトに対してグローバルです。 たとえば、`My.Application.Info` は、アプリケーション全体で共有される状態をカプセル化します。
- **単純なパラメーターの型。** 複雑なパラメーターの型を避け、シンプルに保ってください。 代わりに、パラメーター入力を受け取らないメソッド、または文字列、プリミティブ型などの単純な入力型を受け取るメソッドを作成してください。
- **ファクトリ メソッド。** 一部の型は、インスタンス化が困難な場合があります。 ファクトリ メソッドを `My` 名前空間の拡張機能として指定すると、このカテゴリに分類される型をより簡単に検出して使用できます。 適切に機能するファクトリ メソッドの例として、`My.Computer.FileSystem.OpenTextFileReader` があります。 .NET Framework で使用できるいくつかのストリーム型があります。 具体的にテキスト ファイルを指定することによって、`OpenTextFileReader` によりユーザーが使用するストリームを理解できます。

これらのガイドラインでは、クラス ライブラリの一般的な設計原則は使用できません。 むしろ、これらは、Visual Basic と `My` 名前空間を使用している開発者向けに最適化された推奨事項です。 クラス ライブラリを作成するための一般的な設計原則については、「[フレームワーク デザインのガイドライン](../../../standard/design-guidelines/index.md)」を参照してください。

## <a name="packaging-and-deploying-extensions"></a>拡張機能のパッケージ化と配置

Visual Studio プロジェクト テンプレートに `My` 名前空間の拡張機能を含めることができます。また、拡張機能をパッケージ化して Visual Studio 項目テンプレートとして配置することもできます。 `My` 名前空間の拡張機能を Visual Studio 項目テンプレートとしてパッケージ化すると、Visual Basic によって提供される追加機能を利用できます。 これらの機能を使用すると、プロジェクトが特定のアセンブリを参照するときに拡張機能を含めたり、Visual Basic プロジェクト デザイナーの **[My 拡張]** ページを使用して、ユーザーが `My` 名前空間の拡張機能を明示的に追加できるようにしたりできます。

`My` 名前空間の拡張機能を配置する方法の詳細については、「[カスタム My 拡張のパッケージ化と配置](packaging-and-deploying-custom-my-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [カスタム My 拡張のパッケージ化と配置](packaging-and-deploying-custom-my-extensions.md)
- [Visual Basic アプリケーション モデルの拡張](extending-the-visual-basic-application-model.md)
- [My で利用可能なオブジェクトのカスタマイズ](customizing-which-objects-are-available-in-my.md)
- [[マイ拡張] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)
- [[アプリケーション] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [Partial](../../language-reference/modifiers/partial.md)
