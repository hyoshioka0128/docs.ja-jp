---
title: XAML ノード ストリームの構造と概念について
ms.date: 03/30/2017
helpviewer_keywords:
- XAML node streams [XAML Services]
- nodes [XAML Services], XAML node stream
- XAML [XAML Services], XAML node streams
ms.assetid: 7c11abec-1075-474c-9d9b-778e5dab21c3
ms.openlocfilehash: b3de3dca029c5e676fc7cdebc7735cfdade0228a
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432858"
---
# <a name="xaml-node-stream-structures-and-concepts"></a>XAML ノード ストリームの構造と概念

.NET XAML サービスに実装される XAML リーダーと XAML ライターは、XAML ノード ストリームのデザイン概念に基づいています。 XAML ノード ストリームは、一連の XAML ノードを概念化したものです。 この概念化では、XAML プロセッサは、XAML 内のノードのリレーションシップの構造を 1 つずつ処理します。 常に、開いている XAML ノード ストリームに存在する現在のレコードまたは現在の位置は 1 つのみで、API の多くの側面がレポートするのは、その位置から入手できる情報のみです。 XAML ノード ストリームの現在のノードは、オブジェクト、メンバー、または値として記述できます。 XAML を XAML ノード ストリームとして扱うことで、XAML リーダーは XAML ライターと通信するとともに、XAML に関するパスの読み込みまたはパスの保存操作中に、XAML ノード ストリームのコンテンツをプログラムが表示、操作、または変更できるようにします。 XAML リーダーとライターの API デザインと XAML ノード ストリームの概念は、以前に関連するリーダーおよびライターのデザインと概念 (XML<xref:System.Xml.XmlWriter>ドキュメント オブジェクト モデル (DOM) や クラスなど) に<xref:System.Xml.XmlReader>似ています。 このトピックでは、XAML ノード ストリームの概念について説明するとともに、XAML ノード レベルで XAML 表現と対話するルーチンを記述する方法について説明します。

## <a name="loading-xaml-into-a-xaml-reader"></a>XAML リーダーに XAML を読み込む

<xref:System.Xaml.XamlReader> 基底クラスは、初期の XAML を XAML リーダーに読み込む特定の手法を宣言しません。 代わりに、派生クラスが、XAML の一般的な特性と入力ソースの制約などの読み込みの手法を宣言および実装します。 たとえば、 <xref:System.Xaml.XamlObjectReader> は、オブジェクト グラフの読み取りを、ルートまたはベースを表す 1 つのオブジェクトの入力ソースから開始します。 <xref:System.Xaml.XamlObjectReader> はその後、オブジェクト グラフから XAML ノード ストリームを生成します。

最も顕著な .NET XAML<xref:System.Xaml.XamlReader>サービス定義<xref:System.Xaml.XamlXmlReader>のサブクラスは です。 <xref:System.Xaml.XamlXmlReader> は、初期の XAML を、直接ストリームまたはファイルのパスを経由してテキスト ファイル読み込むか、 <xref:System.IO.TextReader>などの関連するリーダー クラスを経由して間接的に読み込みます。 <xref:System.Xaml.XamlReader> は、XAML 入力ソースが読み込まれた後には、その全体を格納していると考えることができます。 ただし、 <xref:System.Xaml.XamlReader> のベース API は、リーダーが XAML の 1 つのノードと対話するように設計されています。 初めて読み込まれるときに表示される最初の 1 つのノードは、XAML のルートとその開始オブジェクトです。

### <a name="the-xaml-node-stream-concept"></a>XAML ノード ストリームの概念

XML ベースのテクノロジへのアクセスに対する DOM、ツリー メタファ、またはクエリ ベースのアプローチに精通している場合は、XAML ノード ストリームを概念化する便利な方法を次に示します。 読み込まれた XAML が、 DOM またはツリーで、可能な限りすべてのノードが幅広く拡張され、直線的に表示されるところを想像してください。 ノードを進んでいくうちに、DOM に関連するレベルの " in" または "out" レベルを走査することがありますが、これらのレベルの概念はノード ストリームと関係がないため、XAML ノード ストリームは明示的に追跡しません。 ノード ストリームには、「現在の」位置がありますが、参照として自分でストリームのその他の部分を格納していない限り、現在のノードの位置を除くノード ストリームのすべての側面は表示されません。

XAML ノード ストリームの概念には、ノード ストリーム全体を通過すると、XAML 表現全体が処理されたことが保証されるという大きな利点があります。情報を処理するためのクエリ、DOM の操作、またはその他の非線形アプローチで、完全な XAML 表現の一部が不足していると心配する必要はありません。 このため、XAML ノード ストリーム表現は、XAML リーダーと XAML ライターの両方の接続、および XAML 処理操作の読み取りと書き込みの各フェーズの間で動作する独自のプロセスを挿入できるシステムを用意するのに最適です。 多くの場合、XAML ノード ストリーム内のノードの順序付けは、順序がソース テキスト、バイナリ、またはオブジェクト グラフで表示されるしくみと比較して、XAML リーダーによって意図的に最適化または表示されます。 この動作は、ノード ストリームにおいて、XAML ライターが「戻る」必要がある位置に存在しない XAML 処理アーキテクチャを適用することを意図しています。 理想としては、すべての XAML の書き込み操作が、スキーマ コンテキストとノード ストリームの現在の位置に基づいて動作できる必要があります。

## <a name="a-basic-reading-node-loop"></a>基本的な読み取りノードのループ

XAML ノード ストリームを検査するための基本的な読み取りノードのループは、次の概念で構成されます。 このトピックで説明したようなノード ループの目的から、 <xref:System.Xaml.XamlXmlReader>を使用して人間が判読できるテキスト ベースの XAML ファイルを読み取ることを想定してください。 このセクションのリンクは、 <xref:System.Xaml.XamlXmlReader>が実装する特別な XAML ノード ループ API を指しています。

- XAML ノード ストリームの終わりになっていないことを確認してください ( <xref:System.Xaml.XamlXmlReader.IsEof%2A>を確認するか、 <xref:System.Xaml.XamlXmlReader.Read%2A> の戻り値を使用します)。 ストリームの終わりになっている場合は、現在のノードはないため、終了する必要があります。

- <xref:System.Xaml.XamlXmlReader.NodeType%2A>を呼び出して、XAML ノード ストリームが現在どのような種類のノードを公開しているかを確認します。

- 直接接続されている、関連する XAML オブジェクト ライターを使用している場合は、通常はこの時点で <xref:System.Xaml.XamlWriter.WriteNode%2A> を呼び出します。

- どの <xref:System.Xaml.XamlNodeType> が現在のノードまたは現在のレコードとして報告されているかに基づいて、次のいずれかを呼び出して、ノードのコンテンツに関する情報を取得します。

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> または <xref:System.Xaml.XamlNodeType.StartMember> の <xref:System.Xaml.XamlNodeType.EndMember>の場合、 <xref:System.Xaml.XamlXmlReader.Member%2A> を呼び出して、メンバーに関する <xref:System.Xaml.XamlMember> の情報を取得します。 メンバーは<xref:System.Xaml.XamlDirective>、 である場合があるため、前のオブジェクトの従来型定義メンバーであるとは限りません。 たとえば、オブジェクトに適用された `x:Name` は XAML メンバーとして表示されます。ここで、 <xref:System.Xaml.XamlMember.IsDirective%2A> は true、メンバーの <xref:System.Xaml.XamlMember.Name%2A> は `Name`で、このディレクティブが XAML 言語の XAML 名前空間の下にあることを示すその他のプロパティがあります。

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> または <xref:System.Xaml.XamlNodeType.StartObject> の <xref:System.Xaml.XamlNodeType.EndObject>の場合は、 <xref:System.Xaml.XamlXmlReader.Type%2A> を呼び出して、オブジェクトに関する <xref:System.Xaml.XamlType> の情報を取得します。

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> の <xref:System.Xaml.XamlNodeType.Value>で、 <xref:System.Xaml.XamlXmlReader.Value%2A>を呼び出します。 ノードがメンバーの最も単純な表現である場合、またはオブジェクトの初期化のテキストである場合のみ、ノードは値になります (ただし、このトピックの以下のセクションに記載する型変換の動作に注意する必要があります)。

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> の <xref:System.Xaml.XamlNodeType.NamespaceDeclaration>の場合は、 <xref:System.Xaml.XamlXmlReader.Namespace%2A> を呼び出して、名前空間ノードの名前空間情報を取得します。

- <xref:System.Xaml.XamlXmlReader.Read%2A> を呼び出して、XAML リーダーを XAML ノード ストリームの次のノードに進め、手順を繰り返します。

.NET XAML サービス XAML リーダーによって提供される XAML ノード ストリームは、常に、すべての可能なノードの完全な、深い走査を提供します。 XAML ノード ループの一般的なフロー制御の手法には、 `while (reader.Read())`内の本文の定義、およびノード ループの各ノード ポイントにおける <xref:System.Xaml.XamlXmlReader.NodeType%2A> の切り替えなどがあります。

ノード ストリームがファイルの終わりにある場合、現在のノードは null です。

リーダーとライターを使用する最も簡単なループは、次の例に似ています。

```csharp
XamlXmlReader xxr = new XamlXmlReader(new StringReader(xamlStringToLoad));
//where xamlStringToLoad is a string of well formed XAML
XamlObjectWriter xow = new XamlObjectWriter(xxr.SchemaContext);
while (xxr.Read()) {
  xow.WriteNode(xxr);
}
```

読み込みパスの XAML ノード ループの基本的な例では、XAML リーダーと XAML ライターが透過的に接続されています。 <xref:System.Xaml.XamlServices.Parse%2A?displayProperty=nameWithType>を使用した場合と違いはありません。 しかし、この基本構造は、読み取りと書き込みのシナリオに適用するように拡張されます。 可能なシナリオは次のとおりです。

- <xref:System.Xaml.XamlXmlReader.NodeType%2A>で切り替える。 読み込まれているノードの型によって、さまざまな操作を実行する。

- どの場合にも <xref:System.Xaml.XamlWriter.WriteNode%2A> を呼び出さない。 一部の <xref:System.Xaml.XamlWriter.WriteNode%2A> の場合のみ <xref:System.Xaml.XamlXmlReader.NodeType%2A> を呼び出す。

- 特定のノード型のロジックで、そのノードの詳細を分析して操作します。 たとえば、特定の XAML 名前空間から取得したオブジェクトのみを記述し、その XAML 名前空間からでないオブジェクトを削除または延期できます。 または、XAML システムがメンバーの処理の一部としてサポートしていないすべての XAML ディレクティブを削除または再処理することができます。

- <xref:System.Xaml.XamlObjectWriter> メソッドをオーバーライドするカスタムの `Write*` を定義します。場合によっては XAML スキーマ コンテキストをバイパスする型マッピングを実行します。

- XAML の動作の違いのカスタマイズをリーダーとライターの両方で使用できるように、 <xref:System.Xaml.XamlXmlReader> を構築して既定以外の XAML スキーマ コンテキストを使用します。

### <a name="accessing-xaml-beyond-the-node-loop-concept"></a>ノード ループの概念を超えた XAML へのアクセス

XAML ノード ループとして使用する以外に XAML 表現を使用する可能性があるその他の方法があります。 たとえば、インデックス付きのノードを読み取ることができる XAML リーダー、特に `x:Name`、 `x:Uid`、またはその他の識別子を介して直接ノードにアクセスする XAML リーダーが存在することがあります。 .NET XAML サービスは完全な実装を提供するわけではありませんが、サービスとサポートの種類を通じて推奨されるパターンを提供します。 詳細については、「 <xref:System.Xaml.IXamlIndexingReader> および <xref:System.Xaml.XamlNodeList>」を参照してください。

## <a name="working-with-the-current-node"></a>現在のノードの操作

XAML ノード ループを使用するほとんどのシナリオは、ノードの読み取りだけを行うわけではありません。 ほとんどのシナリオでは、現在のノードを処理し、 <xref:System.Xaml.XamlWriter>の実装に 1 回に 1 ノードずつ渡します。

一般的な読み込みパスりのシナリオでは、 <xref:System.Xaml.XamlXmlReader> は XAML ノード ストリームを生成します。XAML ノードは、ロジックと XAML スキーマ コンテキストに従って処理され、ノードは <xref:System.Xaml.XamlObjectWriter>に渡されます。 続いて、生成されたオブジェクト グラフをアプリケーションまたはフレームワークに統合します。

一般的な保存パスのシナリオでは、 <xref:System.Xaml.XamlObjectReader> がオブジェクト グラフを読み取り、個々の XAML ノードが処理され、 <xref:System.Xaml.XamlXmlWriter> が XAML テキスト ファイルとしてシリアル化された結果を出力します。 重要なのは、パスとシナリオの両方が一度に 1 つの XAML ノードを使用して作業し、XAML ノードは XAML 型システムとthe.NET XAML サービス API によって定義される標準化された方法で処理できるということです。

### <a name="frames-and-scope"></a>フレームとスコープ

XAML ノード ループは、線形的な方法で XAML ノード ストリーム全体を通過します。 ノード ストリームは、オブジェクト、他のオブジェクトを含むメンバーなどを走査します。 フレームとスタックの概念を実装して XAML ノード ストリーム内のスコープを追跡すると役立つことがよくあります。 ノード ストリームの使用中に積極的に調整する場合は、特に役立ちます。 ノード ループのロジックの一部として実装するフレームとスタックのサポートでは、DOM の観点から構造を考える場合、XAML ノードの構造に下りる際に `StartObject` (または `GetObject`) と `EndObject` スコープをカウントすることがあります。

## <a name="traversing-and-entering-object-nodes"></a>オブジェクトのノードの走査と入力

XAML リーダーによって開かれたときのノード ストリームの最初のノードは、ルート オブジェクトの開始オブジェクト ノードです。 定義上、このオブジェクトは常に 1 つのオブジェクト ノードで、ピアはありません。 現実世界の XAML の例では、ルート オブジェクトがより多くのオブジェクトを保持する 1 つ以上のプロパティを持つように定義されます。これらのプロパティにはメンバー ノードがあります。 メンバー ノードには、1 つ以上のオブジェクト ノードがあるか、代わりに値ノードで終了することもあります。 一般的に、ルート オブジェクトは XAML の名前のスコープを定義します。これは構文的に属性として XAML テキスト マークアップに割り当てられますが、XAML ノード ストリームの表現にある `Namescope` ノードの種類にマップされます。

次の XAML の例を考えてみましょう (これは任意の XAML であり、.NET の既存の型によってサポートされていません)。 このオブジェクト モデルでは、 `FavorCollection` は `List<T>` の `Favor`であること、 `Balloon` と `NoiseMaker` は `Favor`への割り当てが可能であること、 `Balloon.Color` プロパティは `Color` オブジェクトに基づいていること (WPF が色を既知の色の名前として定義する方法に似ています)、および `Color` は属性の構文の型コンバーターをサポートすると想定します。

|XAML マークアップ|結果となる XAML ノード ストリーム|
|-----------------|--------------------------------|
|`<Party`|`Namespace` の `Party`|
|`xmlns="PartyXamlNamespace">`|`StartObject` の `Party`|
|`<Party.Favors>`|`StartMember` の `Party.Favors`|
||暗黙的な`StartObject` の `FavorCollection`ノード|
||暗黙的な`StartMember` 項目のプロパティの `FavorCollection` ノード|
|`<Balloon`|`StartObject` の `Balloon`|
|`Color="Red"`|`StartMember` の `Color`<br /><br /> 属性値の文字列`Value` の `"Red"`ノード<br /><br /> `Color` の `EndMember`|
|`HasHelium="True"`|`StartMember` の `HasHelium`<br /><br /> 属性値の文字列`Value` の `"True"`ノード<br /><br /> `HasHelium` の `EndMember`|
|`>`|`Balloon` の `EndObject`|
|`<NoiseMaker>Loudest</NoiseMaker>`|`StartObject` の `NoiseMaker`<br /><br /> `StartMember` の `_Initialization`<br /><br /> 初期化値の文字列`Value` の `"Loudest"`ノード<br /><br /> `EndMember` の `_Initialization`<br /><br /> `NoiseMaker` の `EndObject`|
||暗黙的な`EndMember` 項目のプロパティの `FavorCollection` ノード|
||暗黙的な`EndObject` の `FavorCollection`ノード|
|`</Party.Favors>`|`Favors` の `EndMember`|
|`</Party>`|`Party` の `EndObject`|

XAML ノード ストリームでは、次の動作に依存することができます。

- `Namespace` ノードが存在する場合は、 `StartObject` で XAML 名前空間を宣言した `xmlns`の直前のストリームに追加されます。 もう一度、XAML と使用例のノード ストリームがある上記の表をご覧ください。 `StartObject` ノードと `Namespace` ノードがテキストのマークアップでそれらの宣言の位置とどのように入れ替えられているかに注意してください。 これは、ノード ストリームで、名前空間ノードが常に適用するノードの前に表示される動作の典型です。 この設計の目的は、名前空間情報は、オブジェクト ライターにとって重要であり、オブジェクト ライターが型のマッピングの実行を試みる前 (そうでなければオブジェクトを処理する前) に知らされる必要があるということです。 ストリームで XAML 名前空間の情報をアプリケーションのスコープの前に配置すると、ノード ストリームを常に表示された順序で処理することが簡単になります。

- 前述の考慮事項により、ノードをルートの `Namespace` からではなく最初から走査する場合、ほとんどの現実世界のマークアップのケースで最初に読み取る `StartObject` ノードは 1 つ以上になります。

- `StartObject` ノードの後には `StartMember`、 `Value`、またはすぐに `EndObject`が続きます。 別の `StartObject`がすぐに続くことはありません。

- `StartMember` の後には `StartObject`、 `Value`、またはすぐに `EndMember`が続きます。 新しい値をインスタンス化する `GetObject`ではなく、値が親オブジェクトの既存の値に由来すると想定されるメンバーの場合は、後に `StartObject` が続きます。 また、 `Namespace` ノードも後に続きます。このノードは今後の `StartObject`に適用されます。 別の `StartMember`がすぐに続くことはありません。

- `Value` ノードは値自体を表します。 "EndValue" はありません。 後には `EndMember`のみが続きます。

  - 構築で使用される可能性があるオブジェクトの XAML 初期化テキストは、オブジェクト - 値構造の結果にはなりません。 代わりに、 `_Initialization` という名前のメンバーの専用のメンバー ノードが作成されます。 そのメンバー ノードには、初期化値の文字列が含まれています。 存在する場合は、 `_Initialization` が常に最初の `StartMember`になります。 一部の XAML サービス表記では、`_Initialization` が XAML 言語の XAML 名前スコープで修飾して、 `_Initialization` がバッキング タイプで定義されたプロパティでないことを明確にすることがあります。

  - メンバーと値の組み合わせは、値の属性設定を表します。 結局、この値の処理に関係する値コンバーターが使用されることがあり、値はプレーン文字列になります。 ただし、これは XAML オブジェクト ライターがこのノード ストリームを処理するまで評価されません。 XAML オブジェクト ライターには、必要な XAML スキーマ コンテキスト、型システムのマッピング、および値の変換に必要なその他のサポートが用意されています。

- `EndMember` ノードの後には、後続のメンバーとして `StartMember` ノード、またはメンバーの所有者として `EndObject` ノードが続きます。

- `EndObject` ノードの後には、 `EndMember` ノードが続きます。 さらに、オブジェクトがコレクション アイテムのピアである場合は、 `StartObject` ノードが後に続くこともあります。 または、 `Namespace` ノードが後に続きます。このノードは今後の `StartObject`に適用されます。

  - ノード ストリーム全体を閉じるという独特なケースでは、ルートの `EndObject` の後には何も続きません。リーダーはファイルの終わりになり、 <xref:System.Xaml.XamlReader.Read%2A> は `false`を返します。

## <a name="value-converters-and-the-xaml-node-stream"></a>値コンバーターと XAML ノード ストリーム

値コンバーターとは、マークアップ拡張機能、型コンバーター (値のシリアライザーを含む)、または XAML 型システムを介して値コンバーターとして報告されている別の専用のクラスの一般用語です。 XAML ノード ストリームでは、型コンバーターの使用法と、マークアップ拡張機能の使用法では、表現が非常に異なります。

### <a name="type-converters-in-the-xaml-node-stream"></a>XAML ノード ストリームでの型コンバーター

最終的に型コンバーターの使用になる属性セットは、メンバーの値として XAML ノード ストリームで報告されます。 XAML ノード ストリームは、型コンバーター インスタンス オブジェクトを生成してこれに値を渡そうとはしません。 型コンバーターの変換の実装を使用するには、XAML スキーマ コンテキストを呼び出して、型マッピングに使用する必要があります。 値の処理にどの型コンバーターのクラスを使用する必要があるかを決定する場合でも、XAML スキーマ コンテキストが間接的に必要になります。 既定の XAML スキーマ コンテキストを使用する場合は、対象の情報は XAML 型システムから使用できます。 XAML ライターへの接続の前に XAML ノード ストリーム レベルで型コンバーター クラスの情報が必要な場合、設定されているメンバーの <xref:System.Xaml.XamlMember> 情報から取得することができます。 ただし、型コンバーターの入力は、型マッピング システムと XAML スキーマ コンテキストを必要とする操作の残りの部分が実行されるまで (たとえば、XAML オブジェクト ライターによるオブジェクトの作成) まで、XAML ノード ストリームでプレーン値として保持する必要があります。

たとえば、次のクラス定義の概要とそれに対する XAML の使用を検討してください。

```csharp
public class BoardSizeConverter : TypeConverter {
  //converts from string to an int[2] by splitting on an "x" char
}
public class GameBoard {
  [TypeConverter(typeof(BoardSizeConverter))]
  public int[] BoardSize; //2x2 array, initialization not shown
}
```

```xaml
<GameBoard BoardSize="8x8"/>
```

この使用法向けの XAML ノード ストリームのテキスト表現は、次のように表現できます。

`StartObject` を表す <xref:System.Xaml.XamlType> と `GameBoard`

`StartMember` を表す <xref:System.Xaml.XamlMember> と `BoardSize`

テキスト文字列 "`Value` " がある`8x8`ノード

`EndMember` と一致する `BoardSize`

`EndObject` と一致する `GameBoard`

このノード ストリームには型コンバーター インスタンスがないことに注意してください。 ただし、 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=nameWithType> の <xref:System.Xaml.XamlMember> で `BoardSize`を呼び出して、型コンバーター情報を取得することができます。 有効な XAML スキーマ コンテキストがある場合は、 <xref:System.Xaml.Schema.XamlValueConverter%601.ConverterInstance%2A>からインスタンスを取得することでコンバーターのメソッドを呼び出すこともできます。

### <a name="markup-extensions-in-the-xaml-node-stream"></a>XAML ノード ストリームのマークアップ拡張機能

マークアップ拡張機能の使用状況は、メンバー内のオブジェクト ノードとして XAML ノード ストリームで報告されます。ここで、オブジェクトはマークアップ拡張機能のインスタンスを表します。 そのため、マークアップ拡張機能の使用法は、型コンバーターの使用法より明示的にノード ストリームの表現で表され、より多くの情報を伝達できます。 <xref:System.Xaml.XamlMember> の情報では、マークアップ拡張機能について何も述べることができませんでした。これは、使用法が状況に左右され、可能な各マークアップのケースで異なるためです。型コンバーターの場合のようには、使用法が型またはメンバーごとに専用かつ暗黙的なのではありません。

オブジェクトのノードとしてのマークアップ拡張機能のノード ストリームの表現は、マークアップ拡張機能の使用法が XAML テキスト マークアップ内の属性の形式である場合でも該当します (多くの場合該当します)。 明示的なオブジェクトの要素の形式を使用するマークアップ拡張機能の使用法は同じように扱われます。

マークアップ拡張機能のオブジェクト ノード内には、そのマークアップ拡張機能のメンバーが存在する可能性があります。 XAML ノード ストリームの表現では、位置指定のパラメーターの使用法か、明示的な名前付きパラメーターの使用法によって、そのマークアップ拡張機能の使用法が維持されます。

位置指定のパラメーターの使用法の場合、XAML ノード ストリームには、使用状況を記録する、XAML 言語で定義されたプロパティ `_PositionalParameters` が含まれます。 このプロパティは、 <xref:System.Collections.Generic.List%601> 制約が付いたジェネリック <xref:System.Object> です。 制約は、オブジェクトであり、文字列ではありません。位置指定のパラメーターの使用法では、場合によって、そのパラメーターの中に入れ子になったマークアップ拡張機能の使用法が含まれている可能性があるためです。 使用法から位置指定のパラメーターにアクセスするため、リストを反復処理してから、個々のリストの値にインデクサーを使用することがあります。

名前付きパラメーターの使用法では、名前付きの各パラメーターは、ノード ストリームでその名前のメンバー ノードとして表されます。 メンバー値は必ずしも文字列とは限りません。入れ子になったマークアップ拡張機能の使用の可能性があるためです。

`ProvideValue` はマークアップ拡張機能から、まだ呼び出されていません。 ただし、ノード ストリームで `WriteEndObject` を確認する際、マークアップ拡張機能ノードで呼び出されるように XAML リーダーと XAML ライターを接続する場合はこれが呼び出されます。 このため、通常は、読み込みパスでオブジェクト グラフを形成するために使用するのと同じ XAML スキーマのコンテキストが使用できる必要があります。 それ以外の場合、すべてのマークアップ拡張機能の `ProvideValue` は、期待されるサービスが使用可能でないため、ここで例外をスローする可能性があります。

## <a name="xaml-and-xml-language-defined-members-in-the-xaml-node-stream"></a>XAML ノード ストリームにおける XAML および XML 言語で定義されたメンバー

明示的な <xref:System.Xaml.XamlMember> の検索または構築を介してではなく、XAML リーダーの解釈と規約のため、特定のメンバーが XAML ノード ストリームに導入されています。 多くの場合、これらのメンバーは XAML ディレクティブです。 場合によっては、XAML ノード ストリームにディレクティブを導入する XAML の読み取りの動作になります。 つまり、元の入力 XAML テキストはメンバー ディレクティブを明示的に指定しませんでしたが、XAML リーダーは、その情報が失われる前に、構造上の XAML 規則を満たし、XAML ノード ストリームの情報を報告するためにディレクティブを挿入します。

次のリストでは、XAML リーダーがディレクティブ XAML メンバー ノードを導入する必要があるすべてのケースと、.NET XAML サービスの実装でそのメンバー ノードを識別する方法について説明します。

- **オブジェクト ノードの初期化テキスト:** このメンバー ノードの名前は `_Initialization`です。この名前は XAML ディレクティブを表し、XAML 言語の XAML 名前空間で定義されます。 その静的なエンティティは <xref:System.Xaml.XamlLanguage.Initialization%2A>から取得できます。

- **マークアップ拡張機能の位置指定パラメーター:** このメンバー ノードの名前は `_PositionalParameters`です。この名前は、XAML 言語の XAML 名前空間で定義されます。 それには常にオブジェクトのジェネリック リストが含まれ、それぞれが入力 XAML で指定される `,` 区切り文字で分割して事前に分離された位置指定パラメーターになっています。 <xref:System.Xaml.XamlLanguage.PositionalParameters%2A>から、位置指定パラメーター ディレクティブの静的なエンティティを取得できます。

- **不明なコンテンツ:** このメンバー ノードの名前は `_UnknownContent`です。 厳密に言うと、これは <xref:System.Xaml.XamlDirective>で、XAML 言語の XAML 名前空間で定義されます。 このディレクティブは、XAML オブジェクト要素にソース XAML のコンテンツが含まれている場合は sentinel として使用されますが、現在使用できる XAML スキーマ コンテキストで決定できるコンテンツのプロパティはありません。 `_UnknownContent`という名前のメンバーを確認すると、XAML ノード ストリームでこのケースを検出できます。 読み込みパスの XAML ノード ストリームでその他の処理が行われない場合、いずれかのオブジェクトで <xref:System.Xaml.XamlObjectWriter> のメンバーが検出されると、試行した `WriteEndObject` で既定の `_UnknownContent` がスローされます。 既定の <xref:System.Xaml.XamlXmlWriter> はスローされず、メンバーを暗黙の型として処理します。 `_UnknownContent` の静的なエンティティは <xref:System.Xaml.XamlLanguage.UnknownContent%2A>から取得できます。

- **コレクションのコレクション プロパティ:** XAML で使用されるコレクション クラスのバッキング CLR 型には、通常、コレクション項目を保持する専用の名前付きプロパティがありますが、そのプロパティは、型解決のバッキング前に XAML 型システムに認識されません。 代わりに、XAML ノード ストリームでは、コレクションの XAML 型のメンバーとして `Items` プレース ホルダーを導入します。 NET XAML サービスの実装では、ノード ストリーム内のこのディレクティブまたはメンバーの`_Items`名前は です。 このディレクティブの定数は <xref:System.Xaml.XamlLanguage.Items%2A>から取得できます。

    XAML ノード ストリームには、バッキング型の解決と XAML スキーマ コンテキストに基づいて、構成可能でないことが判明した項目を含む Items プロパティが含まれている場合があることに注意してください。 たとえば、次のように入力します。

- **XML 定義のメンバー:**`xml:base`XML 定義の`xml:lang`メンバー`xml:space`とメンバーは、 という`base``lang`名前`space`の XAML ディレクティブとして報告されます。 これらの名前空間は、XML 名前空間 `http://www.w3.org/XML/1998/namespace`です。 これらのそれぞれの定数は <xref:System.Xaml.XamlLanguage>から取得できます。

## <a name="node-order"></a>ノードの順序

場合によって <xref:System.Xaml.XamlXmlReader> は、マークアップに表示する場合、または XML として処理される場合に、ノードの表示順序と比較して、XAML ノード ストリームの XAML ノードの順序を変更します。 この変更は、 <xref:System.Xaml.XamlObjectWriter> が順方向のみにノード ストリームを処理できるようにノードの順序を指定するために行います。  .NET XAML サービスでは、XAML リーダーは、ノード ストリームの XAML オブジェクト ライター コンシューマーのパフォーマンス最適化として、このタスクを XAML ライターに任すのではなく、ノードの順序を変更します。

特定のディレクティブは、特にオブジェクト要素からオブジェクトを作成するために、より多くの情報を提供することを目的としています。 これらのディレクティブは `Initialization`、 `PositionalParameters`、 `TypeArguments`、 `FactoryMethod`、 `Arguments`です。 .NET XAML サービス XAML リーダーは、次のセクションで説明する理由から、オブジェクトのに続`StartObject`くノード ストリームの最初のメンバーとして、これらのディレクティブを配置しようとします。

### <a name="xamlobjectwriter-behavior-and-node-order"></a>XamlObjectWriter の動作とノードの順序

`StartObject` に対する <xref:System.Xaml.XamlObjectWriter> は、すぐにオブジェクト インスタンスを作成するための XAML オブジェクト ライターへのシグナルであるとは限りません。 XAML には、追加の入力を使用してオブジェクトを初期化し、パラメーターなしのコンストラクターを呼び出して初期オブジェクトを生成し、プロパティの設定だけに依存しないようにする言語機能がいくつか含まれています。 これらの機能には、 <xref:System.Windows.Markup.XamlDeferLoadAttribute>、初期化のテキスト、 [x:TypeArguments](xtypearguments-directive.md)、マークアップ拡張機能の位置指定パラメーター、工場出荷時のメソッド、および関連する [x:Arguments](xarguments-directive.md) ノード (XAML 2009) などがあります。 これらの各ケースは実際のオブジェクトの構築を遅らせるため、ノード ストリームが並べ替えられたため、開始メンバーが検出されたときに、そのオブジェクト型の構築ディレクティブではない場合は、XAML オブジェクト ライターは実際にインスタンスを構築する動作に依存できます。

### <a name="getobject"></a>GetObject

`GetObject` は、XAML オブジェクト ライターが新しいオブジェクトを構築するのではなく、オブジェクトの包含プロパティの値を取得する必要がある XAML ノードを表します。 XAML ノード ストリームで `GetObject` ノードに発生する一般的なケースは、コレクション オブジェクトまたは辞書オブジェクトで、包含するプロパティがバッキング型のオブジェクト モデルで意図的に読み取り専用になる場合です。 このシナリオでは、コレクションまたは辞書は、多くの場合は所有する型の初期化ロジックによって作成および (通常は空に) 初期化されます。

## <a name="see-also"></a>関連項目

- <xref:System.Xaml.XamlObjectReader>
- [XAML サービス](index.md)
- [XAML 名前空間](namespaces.md)
