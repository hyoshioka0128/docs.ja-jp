---
title: .NET で文字エンコーディング クラスを使用する方法
description: .NET で文字エンコーディング クラスを使用する方法について説明します。
ms.date: 12/22/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encoding, understanding
- encoding, choosing
- encoding, fallback strategy
ms.assetid: bf6d9823-4c2d-48af-b280-919c5af66ae9
ms.openlocfilehash: c626e79e7bbcd71c90775df8ee8c4d6570c29125
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290579"
---
# <a name="how-to-use-character-encoding-classes-in-net"></a>.NET で文字エンコーディング クラスを使用する方法

この記事では、.NET に用意されている、さまざまなエンコード スキームを使用してテキストをエンコードおよびデコードするためのクラスの使用方法について説明します。 この手順は、[.NET での文字エンコードの概要](character-encoding-introduction.md)に関する記事を既に読んでいることを前提としています。

## <a name="encoders-and-decoders"></a>エンコーダーとデコーダー

.NET には、さまざまなエンコード システムを使用してテキストをエンコードおよびデコードする、エンコーディング クラスが用意されています。 たとえば、<xref:System.Text.UTF8Encoding> クラスには、UTF-8 へのエンコードと UTF-8 からのデコードに関する規則が記述されています。 .NET では、`string` インスタンスに対して UTF-16 エンコード (<xref:System.Text.UnicodeEncoding> クラスによって表されます) が使用されます。 エンコーダーとデコーダーは、他のエンコード スキームでも使用できます。

エンコードとデコードに検証を含めることもできます。 たとえば、<xref:System.Text.UnicodeEncoding> クラスでは、サロゲート範囲内のすべての `char` インスタンスがチェックされ、有効なサロゲート ペアが構成されていることが確認されます。 エンコーダーが無効な文字を処理する方法や、デコーダーが無効なバイトを処理する方法は、フォールバック ストラテジによって決まります。

> [!WARNING]
> .NET のエンコーディング クラスは、文字データを格納および変換するためのものです。 バイナリ データを文字列形式で格納する目的では使用しないでください。 エンコーディング クラスを使用してバイナリ データを文字列形式に変換すると、使用されているエンコーディングによっては、予期しない動作が発生したり、不正確なデータや破損したデータが生成されたりする可能性があります。 バイナリ データを文字列形式に変換するには、 <xref:System.Convert.ToBase64String%2A?displayProperty=nameWithType> メソッドを使用します。

.NET のすべての文字エンコーディング クラスは、すべての文字エンコーディングに共通の機能を定義する抽象クラスの <xref:System.Text.Encoding?displayProperty=nameWithType> クラスを継承します。 .NET に実装されている個々のエンコーディング オブジェクトにアクセスするには次の方法があります。

- <xref:System.Text.Encoding> クラスの静的プロパティを使います。これらのプロパティは、.NET で使用できる標準の文字エンコーディング (ASCII、UTF-7、UTF-8、UTF-16、および UTF-32) を表すオブジェクトを返します。 たとえば、 <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> プロパティは <xref:System.Text.UnicodeEncoding> オブジェクトを返します。 各オブジェクトでは、エンコードできない文字列とデコードできないバイトを処理するために、置換フォールバックが使用されます 詳細については、「[Replacement Fallback](character-encoding.md#Replacement)」をご覧ください。

- エンコーディングのクラス コンストラクターを呼び出します。 ASCII、UTF-7、UTF-8、UTF-16、および UTF-32 の各エンコーディングのオブジェクトは、この方法でインスタンス化できます。 既定では、各オブジェクトはエンコードできない文字列とデコードできないバイトを処理するために置換フォールバックを使用します。ただし、代わりに例外がスローされるように指定することもできます 詳細については、「[Replacement Fallback](character-encoding.md#Replacement)」および「[Exception Fallback](character-encoding.md#Exception)」セクションをご覧ください。

- <xref:System.Text.Encoding.%23ctor%28System.Int32%29> コンストラクターを呼び出して、エンコーディングを表す整数を渡します。 エンコードできない文字列とデコードできないバイトの処理には、標準エンコーディングのエンコーディング オブジェクトでは置換フォールバックが、コード ページ エンコーディングと 2 バイト文字セット (DBCS) エンコーディングのエンコーディング オブジェクトでは最適フォールバックが使用されます 詳細については、「[Best-Fit Fallback](character-encoding.md#BestFit)」をご覧ください。

- <xref:System.Text.Encoding.GetEncoding%2A?displayProperty=nameWithType> メソッドを呼び出します。このメソッドは、.NET で使用できる任意のエンコーディング (標準、コード ページ、または DBCS) を返します。 オーバーロードを使用すると、エンコーダーおよびデコーダーの両方のフォールバック オブジェクトを指定できます。

.NET で使えるすべてのエンコーディングに関する情報を取得するには、<xref:System.Text.Encoding.GetEncodings%2A?displayProperty=nameWithType> メソッドを呼び出します。 .NET でサポートされている文字エンコード スキームを、次の表に示します。

|エンコーディング クラス|説明|
|--------------|-----------|
|[ASCII](xref:System.Text.ASCIIEncoding)|バイトの下位 7 ビットを使用して、限られた範囲の文字をエンコードします。 ASCII エンコーディングでは、U+0000 から U+007F までの文字値しかサポートされていないため、ほとんどの場合、国際対応アプリケーションでは ASCII エンコーディングの使用は不適切です。|
|[UTF-7](xref:System.Text.UTF7Encoding)|文字を 7 ビット ASCII 文字のシーケンスとして表します。 ASCII 以外の Unicode 文字は、ASCII 文字のエスケープ シーケンスによって表します。 UTF-7 では、メールやニュースグループなどのプロトコルがサポートされています。 ただし、UTF-7 は特に安全でも堅牢でもありません。 場合によっては、1 ビットの変更により、UTF-7 文字列全体の解釈が完全に変わる場合があります。 他の場合には、異なる UTF-7 文字列がエンコードによって同じテキストになる可能性もあります。 ASCII 以外の文字を含むシーケンスの場合、UTF-7 は UTF-8 よりも多くの空間を必要とし、エンコードとデコードに時間がかかります。 したがって、可能であれば、UTF-7 ではなく UTF-8 を使用してください。|
|[UTF-8](xref:System.Text.UTF8Encoding)|各 Unicode コード ポイントが、1 バイトから 4 バイトのシーケンスとして表現されます。 UTF-8 では、8 ビット データ サイズがサポートされており、既存の多くのオペレーティング システムに対応できます。 ASCII 範囲の文字については、UTF-8 は ASCII エンコーディングと一致し、より広範な文字を提供します。 ただし、中国語、日本語、韓国語 (CJK) スクリプトでは、UTF-8 の各文字に 3 バイトが必要となることがあり、データ サイズが UTF-16 より大きくなる可能性があります。 場合によっては、HTML タグなどの ASCII データのサイズによって、CJK 範囲によるサイズの増加が相殺されることがあります。|
|[UTF-16](xref:System.Text.UnicodeEncoding)|各 Unicode コード ポイントが、1 つまたは 2 つの 16 ビット整数のシーケンスとして表現されます。 ほとんどの一般的な Unicode 文字で必要とされる UTF-16 コード ポイントは 1 つだけです。ただし、Unicode の補助文字 (U+10000 以上) には 2 つの UTF-16 サロゲート コード ポイントが必要です。 リトル エンディアンとビッグ エンディアンの両方のバイト順をサポートしています。 UTF-16 エンコーディングは、共通言語ランタイムでは <xref:System.Char> および <xref:System.String> の値を表現するために、Windows オペレーティング システムでは `WCHAR` の値を表現するために使用されています。|
|[UTF-32](xref:System.Text.UTF32Encoding)|各 Unicode コード ポイントが 32 ビット整数として表現されます。 リトル エンディアンとビッグ エンディアンの両方のバイト順をサポートしています。 UTF-32 エンコーディングは、エンコードされた空白がきわめて重要な意味を持つオペレーティング システムで、アプリケーションが UTF-16 エンコーディングのサロゲート コード ポイント動作を回避する必要がある場合に使用します。 ディスプレイ上でレンダリングされる 1 つのグリフも複数の UTF-32 文字でエンコードされることがあります。|
|ANSI/ISO エンコード|さまざまなコード ページがサポートされています。 Windows オペレーティング システムでは、特定の言語または言語グループをサポートするためにコード ページが使用されます。 .NET でサポートされているコード ページの一覧表については、<xref:System.Text.Encoding> クラスを参照してください。 特定のコード ページのエンコーディング オブジェクトを取得するには、 <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> メソッドを呼び出します。 コード ページには、0 から始まる 256 個のコード ポイントが含まれています。 コード ポイント 0 ～ 127 は、ほとんどのコード ページで ASCII 文字セットを表しますが、コード ポイント 128 ～ 255 が表す文字は、コード ページによって異なります。 たとえば、コード ページ 1252 には、英語、ドイツ語、フランス語などのラテン語書記体系の文字を表す文字コードが含まれています。 このコード ページ 1252 の最後の 128 個のコード ポイントには、アクセント記号付き文字が含まれています。 また、コード ページ 1253 には、ギリシャ語書記体系で必要とされる文字コードが含まれています。 このコード ページ 1253 の最後の 128 個のコード ポイントには、ギリシャ文字が含まれています。 このため、ANSI コード ページに依存するアプリケーションでギリシャ語とドイツ語を同じテキスト ストリームに格納する場合には、参照先コード ページを示す識別子を含める必要があります。|
|2 バイト文字セット (DBCS) エンコーディング|中国語、日本語、韓国語など、256 個以上の文字から成る言語をサポートします。 DBCS では、コード ポイントのペア (2 バイト) が 1 つの文字を表します。 DBCS エンコーディングでは、 <xref:System.Text.Encoding.IsSingleByte%2A?displayProperty=nameWithType> プロパティは `false` を返します。 特定の DBCS のエンコーディング オブジェクトを取得するには、 <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> メソッドを呼び出します。 アプリケーションで DBCS データを処理する場合、DBCS 文字の最初のバイト (先頭バイト) は、その後に続く後続バイトと組み合わせて処理されます。 このスキームでは、日本語や中国語など、2 種類の言語を組み合わせて同じデータ ストリームで使用することはできません。これは、2 バイト コード ポイントのペアが表す文字が、コード ページによって異なるためです。|

これらのエンコーディングを使用することにより、Unicode 文字だけでなく、レガシ アプリケーションで最もよく使用されているエンコーディングにも対応できます。 また、 <xref:System.Text.Encoding> から派生するクラスを定義し、そのメンバーをオーバーライドして、カスタム エンコーディングを作成することもできます。

## <a name="net-core-encoding-support"></a>.NET Core でのエンコードのサポート

既定で、.NET Core では、コード ページ 28591 以外のコード ページ エンコーディングや Unicode エンコーディング (UTF-8 や UTF-16 など) を使用できません。 ただし、使うアプリに、.NET を対象とする標準の Windows アプリに含まれているコード ページ エンコーディングを追加できます。 詳細については、「<xref:System.Text.CodePagesEncodingProvider>」を参照してください。

<a name="Selecting"></a>

## <a name="selecting-an-encoding-class"></a>エンコーディング クラスの選択

アプリケーションで使用するエンコーディングを選択できる場合は、Unicode エンコーディング (できれば <xref:System.Text.UTF8Encoding> または <xref:System.Text.UnicodeEncoding>) を使用するようにしてください (.NET でサポートされている Unicode エンコーディングには、そのほかに <xref:System.Text.UTF32Encoding> もあります)。

ASCII エンコーディング (<xref:System.Text.ASCIIEncoding>) を使用しようとしている場合は、代わりに <xref:System.Text.UTF8Encoding> を選択してください。 この 2 つのエンコーディングは、ASCII 文字セットに対する動作は変わりませんが、 <xref:System.Text.UTF8Encoding> には次のような利点があります。

- すべての Unicode 文字を表現できます ( <xref:System.Text.ASCIIEncoding> でサポートされているのは U+0000 ～ U+007F の Unicode 文字値だけです)。

- エラー検出に対応しており、セキュリティも強化されます。

- できるだけ高速になるように調整されているため、他のエンコーディングよりも高速です。 全体が ASCII のコンテンツの場合でも、 <xref:System.Text.UTF8Encoding> で実行される演算は、 <xref:System.Text.ASCIIEncoding>で実行される演算よりも高速になります。

<xref:System.Text.ASCIIEncoding> は、レガシ アプリケーションの場合にのみ使用を検討するようにしてください。 ただし、レガシ アプリケーションでも、次のような理由で <xref:System.Text.UTF8Encoding> の方が適していることもあります (既定の設定の場合)。

- 厳密には ASCII でないコンテンツがアプリケーションに含まれている場合、それを <xref:System.Text.ASCIIEncoding>でエンコードすると、ASCII 以外の各文字は疑問符 (?) としてエンコードされます。 アプリケーションがこのデータをデコードすると、情報は失われます。

- 厳密には ASCII でないコンテンツがアプリケーションに含まれている場合、それを <xref:System.Text.UTF8Encoding>でエンコードすると、結果を ASCII として解釈しようとしても一見理解不能になります。 ただし、アプリケーションがこのデータを UTF-8 デコーダーを使用してデコードすると、データのラウンド トリップが正常に行われます。

Web アプリケーションでは、Web 要求への応答としてクライアントに送信される文字に、クライアントで使用されているエンコーディングが反映されるようにする必要があります。 ほとんどの場合は、ユーザーが期待するエンコーディングでテキストを表示するために、 <xref:System.Web.HttpResponse.ContentEncoding%2A?displayProperty=nameWithType> プロパティを <xref:System.Web.HttpRequest.ContentEncoding%2A?displayProperty=nameWithType> プロパティの戻り値に設定する必要があります。

<a name="Using"></a>

## <a name="using-an-encoding-object"></a>エンコーディング オブジェクトの使用

エンコーダーは、文字列 (通常は Unicode 文字) を対応する数値 (バイト) に変換します。 たとえば、ASCII エンコーダーを使用すると、Unicode 文字を ASCII に変換してコンソールに表示することができます。 この変換を実行するには、 <xref:System.Text.Encoding.GetBytes%2A?displayProperty=nameWithType> メソッドを呼び出します。 エンコードされた文字列を格納するために必要なバイト数をエンコードの実行前に確認するには、 <xref:System.Text.Encoding.GetByteCount%2A> メソッドを呼び出します。

次の例では、1 つのバイト配列を使用して、文字列を 2 つの個別の操作でエンコードしています。 バイト配列内の次の ASCII エンコード済みバイト セットの開始位置を示すインデックスが保持されています。 この例では、 <xref:System.Text.ASCIIEncoding.GetByteCount%28System.String%29?displayProperty=nameWithType> メソッドを呼び出して、エンコードされた文字列を格納するために十分な大きさがバイト配列にあるかどうかを確認します。 次に、 <xref:System.Text.ASCIIEncoding.GetBytes%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Byte%5B%5D%2CSystem.Int32%29?displayProperty=nameWithType> メソッドを呼び出して、文字列の文字をエンコードします。

[!code-csharp[Conceptual.Encoding#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getbytes1.cs#8)]
[!code-vb[Conceptual.Encoding#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getbytes1.vb#8)]

デコーダーは、特定の文字エンコーディングが反映されたバイト配列を、文字配列または文字列の一連の文字に変換します。 バイト配列を文字配列にデコードするには、 <xref:System.Text.Encoding.GetChars%2A?displayProperty=nameWithType> メソッドを呼び出します。 バイト配列を文字列にデコードするには、 <xref:System.Text.Encoding.GetString%2A> メソッドを呼び出します。 デコードされたバイトを格納するために必要な文字数をデコードの実行前に確認するには、 <xref:System.Text.Encoding.GetCharCount%2A> メソッドを呼び出します。

次の例では、3 つの文字列をエンコードした後、1 つの文字配列にデコードしています。 文字配列内の次のデコード済み文字セットの開始位置を示すインデックスが保持されています。 この例では、 <xref:System.Text.ASCIIEncoding.GetCharCount%2A> メソッドを呼び出して、デコードされたすべての文字を格納するために十分な大きさが文字配列にあるかどうかを確認します。 次に、 <xref:System.Text.ASCIIEncoding.GetChars%28System.Byte%5B%5D%2CSystem.Int32%2CSystem.Int32%2CSystem.Char%5B%5D%2CSystem.Int32%29?displayProperty=nameWithType> メソッドを呼び出して、バイト配列をデコードします。

[!code-csharp[Conceptual.Encoding#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getchars1.cs#9)]
[!code-vb[Conceptual.Encoding#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getchars1.vb#9)]

<xref:System.Text.Encoding> から派生するクラスのエンコード メソッドとデコード メソッドは、データ全体を処理するように設計されています。つまり、エンコードまたはデコードするすべてのデータが 1 回のメソッド呼び出しで渡されます。 ただし、場合によっては、データがストリームで提供され、エンコードまたはデコードするデータを複数の読み取り操作で取得しなければならないこともあります。 このような場合は、エンコード操作またはデコード操作で、前回の実行時に保存した状態を呼び出す必要があります。 <xref:System.Text.Encoder> および <xref:System.Text.Decoder> から派生するクラスのメソッドでは、複数のメソッド呼び出しにまたがるエンコード操作とデコード操作を処理できます。

特定のエンコーディングの <xref:System.Text.Encoder> オブジェクトは、そのエンコーディングの <xref:System.Text.Encoding.GetEncoder%2A?displayProperty=nameWithType> プロパティから取得できます。 特定のエンコーディングの <xref:System.Text.Decoder> オブジェクトは、そのエンコーディングの <xref:System.Text.Encoding.GetDecoder%2A?displayProperty=nameWithType> プロパティから取得できます。 デコード操作の場合、 <xref:System.Text.Decoder> から派生するクラスに含まれるのは <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> メソッドだけで、 <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType>に対応するメソッドはありません。

次の例は、Unicode のバイト配列のデコードに <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType> メソッドを使用する場合と <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> メソッドを使用する場合の違いを示しています。 この例では、いくつかの Unicode 文字を含む文字列をファイルにエンコードした後、この 2 つのデコード メソッドを使用して一度に 10 バイトずつデコードしています。 10 番目と 11 番目のバイトに出現するサロゲート ペアは、別のメソッド呼び出しでデコードされます。 出力を見るとわかるように、 <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType> メソッドではこれらのバイトが正しくデコードされず、U+FFFD (REPLACEMENT CHARACTER) に置き換えられます。 一方、 <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> メソッドでは、このバイト配列が正しくデコードされて、元の文字列を取得できます。

[!code-csharp[Conceptual.Encoding#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/stream1.cs#10)]
[!code-vb[Conceptual.Encoding#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/stream1.vb#10)]

<a name="FallbackStrategy"></a>

## <a name="choosing-a-fallback-strategy"></a>フォールバック ストラテジの選択

メソッドから文字のエンコードまたはデコードを行おうとしたときにマッピングが存在しない場合は、失敗したマッピングの処理方法を決めるフォールバック ストラテジを実装する必要があります。 次の 3 種類のフォールバック ストラテジがあります。

- Best-Fit Fallback

- Replacement Fallback

- Exception Fallback

> [!IMPORTANT]
> エンコード操作で最も一般的な問題は、Unicode 文字を特定のコード ページ エンコーディングにマップできない場合に発生します。 デコード操作で最も一般的な問題は、無効なバイト シーケンスを有効な Unicode 文字に変換できない場合に発生します。 そのため、個々のエンコーディング オブジェクトで使用されるフォールバック ストラテジを把握しておく必要があります。 エンコーディング オブジェクトをインスタンス化するときには、可能な限り、そのオブジェクトで使用されるフォールバック ストラテジを指定するようにしてください。

<a name="BestFit"></a>

### <a name="best-fit-fallback"></a>Best-Fit Fallback

ターゲット エンコード内に厳密な一致がない文字について、エンコーダーは類似した文字へのマッピングを試みることができます (最適フォールバックは主にエンコード時の問題であり、デコード時の問題ではありません。 Unicode に正常にマッピングできない文字を含むコード ページはほとんどありません)。最適フォールバックは、<xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> および <xref:System.Text.Encoding.GetEncoding%28System.String%29?displayProperty=nameWithType> の各オーバーロードによって取得されるコード ページ エンコーディングと 2 バイト文字セット エンコーディングの既定のフォールバック ストラテジです。

> [!NOTE]
> .NET の Unicode エンコーディング クラス (<xref:System.Text.UTF8Encoding>、<xref:System.Text.UnicodeEncoding>、および <xref:System.Text.UTF32Encoding>) では、理論上すべての文字セットのすべての文字がサポートされているため、これらのクラスを使用すると最適フォールバックの問題を解消できます。

最適なストラテジはコード ページごとに異なります。 たとえば、全角のアルファベットがより一般的な半角のアルファベットにマッピングされるコード ページもあれば、 そのようなマッピングが行われないコード ページもあります。 積極的な最適ストラテジでも、一部のエンコーディングの一部の文字には可能な対応がない場合があります。 たとえば、中国語の漢字からコード ページ 1252 への適切なマッピングはありません。 その場合は、置換文字列が使用されます。 既定では、この文字列は単一の QUESTION MARK (疑問符) (U+003F) です。

> [!NOTE]
> 最適なストラテジは、詳細には文書化されていません。 ただし、いくつかのコード ページは、[Unicode コンソーシアム](https://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/)の Web サイトで文書化されています。 マッピング ファイルを解釈する方法について詳しくは、そのフォルダーの **readme.txt** ファイルをご覧ください。

次の例では、コード ページ 1252 (西ヨーロッパ言語の Windows コード ページ) を使用して、最適マッピングとその欠点を示しています。 まず、 <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> メソッドを使用して、コード ページ 1252 のエンコーディング オブジェクトを取得します。 このエンコーディング オブジェクトは、サポートされていない Unicode 文字に対して既定で最適マッピングを使用します。 次に、スペースで区切られた 3 つの非 ASCII 文字 (CIRCLED LATIN CAPITAL LETTER S (U+24C8)、SUPERSCRIPT FIVE (U+2075)、および INFINITY (U+221E)) を含む文字列をインスタンス化します。 出力を見るとわかるように、この文字列をエンコードすると、スペースを除く元の 3 つの文字が、QUESTION MARK (U+003F)、DIGIT FIVE (U+0035)、および DIGIT EIGHT (U+0038) に置き換えられます。 DIGIT EIGHT は、サポートされていない INFINITY 文字の代替として最適とは言えません。QUESTION MARK は、元の文字に対応するマッピングがなかったことを示します。

[!code-csharp[Conceptual.Encoding#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1.cs#1)]
[!code-vb[Conceptual.Encoding#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1.vb#1)]

最適マッピングは、Unicode データをコード ページ データにエンコードする <xref:System.Text.Encoding> オブジェクトの既定の動作です。レガシ アプリケーションの中には、この動作に依存するものがあります。 ただし、ほとんどの新しいアプリケーションでは、セキュリティ上の理由から、最適動作の使用を避ける必要があります。 たとえば、アプリケーションで、最適エンコードを使用してドメイン名を付けないでください。

> [!NOTE]
> エンコーディングに対してカスタムの最適フォールバック マッピングを実装することもできます。 詳しくは、「 [Implementing a Custom Fallback Strategy](character-encoding.md#Custom) 」セクションをご覧ください。

エンコーディング オブジェクトの既定のフォールバック ストラテジが最適フォールバックである場合、 <xref:System.Text.Encoding> オブジェクトを取得するときに別のフォールバック ストラテジを選択することもできます。そのためには、 <xref:System.Text.Encoding.GetEncoding%28System.Int32%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> または <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> のオーバーロードを呼び出します。 次のセクションでは、コード ページ 1252 にマップできない文字をアスタリスク (*) に置き換える例を紹介します。

[!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
[!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]

<a name="Replacement"></a>

### <a name="replacement-fallback"></a>Replacement Fallback

ターゲット スキームに厳密な一致がなく、マップできる適切な文字もない文字について、アプリケーションで置換文字または置換文字列を指定することができます。 これは Unicode デコーダーの既定の動作です。Unicode デコーダーでは、デコードできない 2 バイトのシーケンスが REPLACEMENT_CHARACTER (U+FFFD) に置き換えられます。 また、 <xref:System.Text.ASCIIEncoding> クラスの既定の動作でもあり、その場合はエンコードまたはデコードできない文字が疑問符に置き換えられます。 次の例は、前の例の Unicode 文字列に対する文字置換を示しています。 出力を見るとわかるように、ASCII バイト値にデコードできない文字は 0x3F (疑問符に対応する ASCII コード) に置き換えられます。

[!code-csharp[Conceptual.Encoding#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/replacementascii.cs#2)]
[!code-vb[Conceptual.Encoding#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/replacementascii.vb#2)]

.NET には、エンコード操作またはデコード操作で正確にマップできない文字を置換文字列に置き換える <xref:System.Text.EncoderReplacementFallback> クラスと <xref:System.Text.DecoderReplacementFallback> クラスが含まれています。 この置換文字列は、既定では疑問符ですが、クラス コンストラクターのオーバーロードを呼び出して別の文字列を選択することもできます。 通常は単一の文字を使用しますが、単一でなくてもかまいません。 次の例では、置換文字列としてアスタリスク (*) を使用する <xref:System.Text.EncoderReplacementFallback> オブジェクトをインスタンス化して、コード ページ 1252 のエンコーダーの動作を変更しています。

[!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
[!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]

> [!NOTE]
> エンコーディング用の置換クラスを実装することもできます。 詳しくは、「 [Implementing a Custom Fallback Strategy](character-encoding.md#Custom) 」セクションをご覧ください。

置換文字列としては、QUESTION MARK (U+003F) のほか、特に Unicode 文字列に正しく変換できないバイト シーケンスをデコードする場合に、Unicode REPLACEMENT CHARACTER (U+FFFD) がよく使用されます。 ただし、置換文字列は自由に選択できます。置換文字列に複数の文字を含めることもできます。

<a name="Exception"></a>

### <a name="exception-fallback"></a>Exception Fallback

最適フォールバックや置換文字列を提供する代わりに、エンコーダーで一連の文字をエンコードできない場合に <xref:System.Text.EncoderFallbackException> をスローしたり、デコーダーでバイト配列をデコードできない場合に <xref:System.Text.DecoderFallbackException> をスローしたりすることもできます。 エンコード操作およびデコード操作で例外をスローするには、 <xref:System.Text.EncoderExceptionFallback> メソッドに <xref:System.Text.DecoderExceptionFallback> オブジェクトおよび <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> オブジェクトを渡します。 次の例は、 <xref:System.Text.ASCIIEncoding> クラスによる例外フォールバックを示しています。

[!code-csharp[Conceptual.Encoding#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/exceptionascii.cs#4)]
[!code-vb[Conceptual.Encoding#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/exceptionascii.vb#4)]

> [!NOTE]
> エンコード操作用のカスタム例外ハンドラーを実装することもできます。 詳しくは、「 [Implementing a Custom Fallback Strategy](character-encoding.md#Custom) 」セクションをご覧ください。

<xref:System.Text.EncoderFallbackException> オブジェクトと <xref:System.Text.DecoderFallbackException> オブジェクトは、例外を引き起こした状況について以下の情報を提供します。

- <xref:System.Text.EncoderFallbackException> オブジェクトに含まれている <xref:System.Text.EncoderFallbackException.IsUnknownSurrogate%2A> メソッドにより、エンコードできない文字が不明なサロゲート ペアか (この場合は `true`が返されます)、不明な単一文字か (この場合は `false`が返されます) が示されます。 サロゲート ペアの文字は、 <xref:System.Text.EncoderFallbackException.CharUnknownHigh%2A?displayProperty=nameWithType> プロパティと <xref:System.Text.EncoderFallbackException.CharUnknownLow%2A?displayProperty=nameWithType> プロパティから取得できます。 不明な単一文字は、 <xref:System.Text.EncoderFallbackException.CharUnknown%2A?displayProperty=nameWithType> プロパティから取得できます。 また、 <xref:System.Text.EncoderFallbackException.Index%2A?displayProperty=nameWithType> プロパティにより、エンコードできない最初の文字が見つかった文字列内の位置が示されます。

- <xref:System.Text.DecoderFallbackException> オブジェクトに含まれている <xref:System.Text.DecoderFallbackException.BytesUnknown%2A> プロパティにより、デコードできないバイト配列が返されます。 また、 <xref:System.Text.DecoderFallbackException.Index%2A?displayProperty=nameWithType> プロパティにより、不明なバイトの開始位置が示されます。

<xref:System.Text.EncoderFallbackException> オブジェクトと <xref:System.Text.DecoderFallbackException> オブジェクトでは、例外に関する診断情報は十分に入手できますが、エンコード バッファーやデコード バッファーにアクセスすることはできません。 したがって、エンコード メソッド内またはデコード メソッド内で無効なデータを置換したり修正したりすることはできません。

<a name="Custom"></a>

## <a name="implementing-a-custom-fallback-strategy"></a>Implementing a Custom Fallback Strategy

.NET には、コード ページによって内部的に実装される最適マッピングに加えて、フォールバック ストラテジを実装するための次のクラスが含まれています。

- <xref:System.Text.EncoderReplacementFallback> および <xref:System.Text.EncoderReplacementFallbackBuffer> 。エンコード操作中に文字を置換します。

- <xref:System.Text.DecoderReplacementFallback> および <xref:System.Text.DecoderReplacementFallbackBuffer> 。デコード操作中に文字を置換します。

- <xref:System.Text.EncoderExceptionFallback> および <xref:System.Text.EncoderExceptionFallbackBuffer> 。文字をエンコードできない場合に <xref:System.Text.EncoderFallbackException> をスローします。

- <xref:System.Text.DecoderExceptionFallback> および <xref:System.Text.DecoderExceptionFallbackBuffer> 。文字をデコードできない場合に <xref:System.Text.DecoderFallbackException> をスローします。

さらに、次の手順に従って、最適フォールバック、置換フォールバック、または例外フォールバックを使用するカスタム ソリューションを実装できます。

1. エンコード操作の場合は <xref:System.Text.EncoderFallback> 、デコード操作の場合は <xref:System.Text.DecoderFallback> の派生クラスを作成します。

2. エンコード操作の場合は <xref:System.Text.EncoderFallbackBuffer> 、デコード操作の場合は <xref:System.Text.DecoderFallbackBuffer> の派生クラスを作成します。

3. 例外フォールバックにおいて、あらかじめ定義されている <xref:System.Text.EncoderFallbackException> クラスと <xref:System.Text.DecoderFallbackException> クラスが目的に合わない場合は、 <xref:System.Exception> や <xref:System.ArgumentException>などの例外オブジェクトから派生クラスを作成します。

### <a name="deriving-from-encoderfallback-or-decoderfallback"></a>EncoderFallback または DecoderFallback からの派生

カスタム フォールバック ソリューションを実装するには、エンコード操作の場合は <xref:System.Text.EncoderFallback> 、デコード操作の場合は <xref:System.Text.DecoderFallback> を継承するクラスを作成する必要があります。 これらのクラスのインスタンスは <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> メソッドに渡され、エンコーディング クラスとフォールバックの実装の仲介役として機能します。

エンコーダーまたはデコーダーのカスタム フォールバック ソリューションを作成するときには、次のメンバーを実装する必要があります。

- <xref:System.Text.EncoderFallback.MaxCharCount%2A?displayProperty=nameWithType> プロパティまたは <xref:System.Text.DecoderFallback.MaxCharCount%2A?displayProperty=nameWithType> プロパティ。最適、置換、例外の各フォールバックで単一の文字を置き換えるために返すことのできる文字の最大数を返します。 カスタム例外フォールバックの場合は 0 になります。

- <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> メソッド。 <xref:System.Text.EncoderFallbackBuffer> または <xref:System.Text.DecoderFallbackBuffer> のカスタム実装を返します。 このメソッドは、エンコーダーで正しくエンコードできない文字が初めて検出されたとき、またはデコーダーで正しくデコードできないバイトが初めて検出されたときに呼び出されます。

### <a name="deriving-from-encoderfallbackbuffer-or-decoderfallbackbuffer"></a>EncoderFallbackBuffer または DecoderFallbackBuffer からの派生

カスタム フォールバック ソリューションを実装するには、エンコード操作の場合は <xref:System.Text.EncoderFallbackBuffer> 、デコード操作の場合は <xref:System.Text.DecoderFallbackBuffer> を継承するクラスを作成する必要もあります。 これらのクラスのインスタンスは、 <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A> クラスおよび <xref:System.Text.EncoderFallback> クラスの <xref:System.Text.DecoderFallback> メソッドによって返されます。 <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> メソッドは、エンコーダーでエンコードできない文字が初めて検出されたときに呼び出され、 <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> メソッドは、デコーダーでデコードできないバイトが検出されたときに呼び出されます。 <xref:System.Text.EncoderFallbackBuffer> クラスと <xref:System.Text.DecoderFallbackBuffer> クラスは、フォールバックの実装を提供します。 各インスタンスは、エンコードできない文字またはデコードできないバイト シーケンスを置き換えるフォールバック文字を含むバッファーを表します。

エンコーダーまたはデコーダーのカスタム フォールバック ソリューションを作成するときには、次のメンバーを実装する必要があります。

- <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> メソッド。 <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> は、エンコーダーによって呼び出され、エンコードできない文字に関する情報をフォールバック バッファーに提供します。 エンコードされる文字はサロゲート ペアである場合もあるため、このメソッドはオーバーロードされます。 最初のオーバーロードには、エンコードされる文字と、その文字列内のインデックスが渡されます。 2 番目のオーバーロードには、上位および下位のサロゲートと、その文字列内のインデックスが渡されます。 <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> メソッドは、デコーダーによって呼び出され、デコードできないバイトに関する情報をフォールバック バッファーに提供します。 このメソッドには、デコードできないバイト配列と、最初のバイトのインデックスが渡されます。 フォールバック メソッドは、フォールバック バッファーが最適な文字または置換文字を提供できる場合は `true` 、それ以外の場合は `false`を返します。 例外フォールバックの場合は例外をスローします。

- <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Text.DecoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> メソッド。フォールバック バッファーから次の文字を取得するために、エンコーダーまたはデコーダーによって繰り返し呼び出されます。 すべてのフォールバック文字を返し終わったら、このメソッドは U+0000 を返す必要があります。

- <xref:System.Text.EncoderFallbackBuffer.Remaining%2A?displayProperty=nameWithType> プロパティまたは <xref:System.Text.DecoderFallbackBuffer.Remaining%2A?displayProperty=nameWithType> プロパティ。フォールバック バッファー内の残りの文字数を返します。

- <xref:System.Text.EncoderFallbackBuffer.MovePrevious%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Text.DecoderFallbackBuffer.MovePrevious%2A?displayProperty=nameWithType> メソッド。フォールバック バッファー内の現在の位置を前の文字に移動します。

- <xref:System.Text.EncoderFallbackBuffer.Reset%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Text.DecoderFallbackBuffer.Reset%2A?displayProperty=nameWithType> メソッド。フォールバック バッファーを再初期化します。

フォールバックの実装が最適フォールバックまたは置換フォールバックの場合は、 <xref:System.Text.EncoderFallbackBuffer> と <xref:System.Text.DecoderFallbackBuffer> の派生クラスで、2 つのプライベート インスタンス フィールド (バッファー内の正確な文字数と、次に返される文字のインデックス) も保持します。

### <a name="an-encoderfallback-example"></a>EncoderFallback の例

前の例では、置換フォールバックを使用して、対応する ASCII 文字がない Unicode 文字をアスタリスク (*) に置き換えました。 次の例では、代わりに最適フォールバックのカスタム実装を使用して、非 ASCII 文字のマッピングを改善しています。

次のコードでは、 `CustomMapper` から派生する <xref:System.Text.EncoderFallback> という名前のクラスを定義して、非 ASCII 文字の最適マッピングを処理します。 このクラスの `CreateFallbackBuffer` メソッドは、 `CustomMapperFallbackBuffer` の実装を提供する <xref:System.Text.EncoderFallbackBuffer> オブジェクトを返します。 `CustomMapper` クラスは、 <xref:System.Collections.Generic.Dictionary%602> オブジェクトを使用して、サポートされていない Unicode 文字 (キー値) と、それらに対応する 8 ビット文字とのマッピングを格納します (64 ビット整数の 2 つの連続するバイトに格納されます)。 このマッピングをフォールバック バッファーで使用できるようにするには、 `CustomMapper` のインスタンスを `CustomMapperFallbackBuffer` のクラス コンストラクターにパラメーターとして渡します。 最も長いマッピングは Unicode 文字 U+221E に対応する文字列 "INF" なので、 `MaxCharCount` プロパティは 3 を返します。

[!code-csharp[Conceptual.Encoding#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#5)]
[!code-vb[Conceptual.Encoding#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#5)]

次のコードでは、 `CustomMapperFallbackBuffer` から派生する <xref:System.Text.EncoderFallbackBuffer>クラスを定義しています。 `CustomMapper` インスタンスで定義されている、最適マッピングを含むディクショナリは、クラス コンストラクターから取得できます。 このクラスの `Fallback` メソッドは、ASCII エンコーダーでエンコードできない Unicode 文字がマッピング ディクショナリで定義されている場合は `true` を返し、それ以外の場合は `false`を返します。 フォールバックのたびに、プライベート変数 `count` は返される残りの文字数を示し、プライベート変数 `index` は次に返される文字の文字列バッファー内 ( `charsToReturn`内) の位置を示します。

[!code-csharp[Conceptual.Encoding#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#6)]
[!code-vb[Conceptual.Encoding#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#6)]

次のコードでは、 `CustomMapper` オブジェクトをインスタンス化して、そのインスタンスを <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> メソッドに渡しています。 出力を見るとわかるように、この最適フォールバックの実装では、元の文字列の 3 つの非 ASCII 文字が正しく処理されます。

[!code-csharp[Conceptual.Encoding#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#7)]
[!code-vb[Conceptual.Encoding#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#7)]

## <a name="see-also"></a>関連項目

- [.NET での文字エンコードの概要](character-encoding-introduction.md)
- <xref:System.Text.Encoder>
- <xref:System.Text.Decoder>
- <xref:System.Text.DecoderFallback>
- <xref:System.Text.Encoding>
- <xref:System.Text.EncoderFallback>
- [グローバライズとローカライズ](../globalization-localization/index.md)
