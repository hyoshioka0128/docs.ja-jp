---
title: XML Schema Definition Tool (Xsd.exe)
description: XML シリアライザー ジェネレーター ツールは、指定されたアセンブリ内の型の XML シリアル化アセンブリを生成します。これにより、XmlSerializer の起動パフォーマンスが向上します。
ms.date: 03/30/2017
ms.assetid: a6e6e65c-347f-4494-9457-653bf29baac2
ms.openlocfilehash: 0275ecfebd427feb104013024654d4a0bc98748a
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84288980"
---
# <a name="xml-schema-definition-tool-xsdexe"></a>XML Schema Definition Tool (Xsd.exe)

XML スキーマ定義ツール (Xsd.exe) は、XDR、XML、および XSD ファイル、またはランタイム アセンブリ内のクラスから XML スキーマ クラスまたは共通言語ランタイム クラスを生成します。

通常、XML スキーマ定義ツール (Xsd.exe) は、次のパスにあります。
_C:\\Program Files (x86)\\Microsoft SDKs\\Windows\\{version}\\bin\\NETFX {version} Tools\\_

## <a name="syntax"></a>構文

コマンド ラインでツールを実行します。

```console
xsd file.xdr [-outputdir:directory][/parameters:file.xml]
xsd file.xml [-outputdir:directory] [/parameters:file.xml]
xsd file.xsd {/classes | /dataset} [/element:element]
             [/enableLinqDataSet] [/language:language]
                          [/namespace:namespace] [-outputdir:directory] [URI:uri]
                          [/parameters:file.xml]
xsd {file.dll | file.exe} [-outputdir:directory] [/type:typename [...]][/parameters:file.xml]
```
  
> [!TIP]
> .NET Framework ツールが適切に機能するには、 `Path`、`Include`、および `Lib` の各環境変数を正しく設定する必要があります。 これらの環境変数を設定するには、\<SDK>\v2.0\Bin ディレクトリにある SDKVars.bat を実行します。 SDKVars.bat は、コマンド シェルごとに実行する必要があります。

## <a name="argument"></a>引数

|引数|説明|
|--------------|-----------------|
|*file.extension*|変換元の入力ファイルを指定します。 拡張子として、.xdr、.xml、.xsd、.dll、または .exe のいずれかを指定する必要があります。<br /><br /> XDR スキーマ ファイル (拡張子 .xdr) を指定すると、Xsd.exe は XDR スキーマを XSD スキーマに変換します。 出力ファイルの名前は XDR スキーマと同じですが、拡張子は .xsd となります。<br /><br /> XML ファイル (拡張子 .xml) を指定すると、Xsd.exe はそのファイル内のデータからスキーマを推測して XSD スキーマを生成します。 出力ファイルの名前は XML ファイルと同じですが、拡張子は .xsd となります。<br /><br /> XML スキーマ ファイル (拡張子 .xsd) を指定すると、XML スキーマと対応するランタイム オブジェクト用のソース コードが生成されます。<br /><br /> ランタイム アセンブリ ファイル (拡張子 .exe または .dll) を指定すると、そのアセンブリに含まれる 1 つ以上の型用のスキーマが生成されます。 `/type` オプションを使用して、スキーマを生成する対象の型を指定できます。 出力スキーマには、schema0.xsd、schema1.xsd などの名前が付けられます。 Xsd.exe が複数のスキーマを生成するのは、指定した型によって、カスタム属性 `XMLRoot` を使用する名前空間が特定される場合のみです。|

## <a name="general-options"></a>一般オプション

|オプション|説明|
|------------|-----------------|
|**/h\[elp\]**|このツールのコマンド構文とオプションを表示します。|
|**/o\[utputdir\]:** _directory_|出力ファイル用のディレクトリを指定します。 この引数は 1 回だけ指定できます。 既定値は、現在のディレクトリです。|
|**/?**|このツールのコマンド構文とオプションを表示します。|
|**/p\[arameters\]:** _file.xml_|指定された .xml ファイルから各種のオペレーション モードのためのオプションを読み込みます。 短縮形は `/p:` です。 詳細については、「[解説](#remarks)」を参照してください。|

## <a name="xsd-file-options"></a>XSD ファイルのオプション
 .xsd ファイルについては、次のオプションのうち 1 つだけを指定する必要があります。

|オプション|説明|
|------------|-----------------|
|**/c\[lasses\]**|指定したスキーマと対応するクラスを生成します。 オブジェクトに XML データを読み込むには、<xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A?displayProperty=nameWithType> メソッドを使用します。|
|**/d\[ataset\]**|指定したスキーマに対応する <xref:System.Data.DataSet> から派生したクラスを生成します。 派生したクラスに XML データを読み込むには、<xref:System.Data.DataSet.ReadXml%2A?displayProperty=nameWithType> メソッドを使用します。|

 .xsd ファイルについては、次のオプションのうち任意のオプションを指定できます。

|オプション|説明|
|------------|-----------------|
|**/e\[lement\]:** _element_|コードを生成する対象とする、スキーマ内の要素を指定します。 既定では、すべての要素が指定されます。 この引数は、複数回指定できます。|
|**/enableDataBinding**|データ バインディングを有効にするために、生成されたすべての型に <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装します。 短縮形は `/edb` です。|
|**/enableLinqDataSet**|(短縮形: `/eld`)LINQ to DataSet を使用して、生成された DataSet を照会できるように指定します。 このオプションは /dataset オプションも指定した場合に使用されます。 詳細については、「[LINQ to DataSet Overview](../../framework/data/adonet/linq-to-dataset-overview.md)」(LINQ to DataSet Overview) と「[Querying Typed DataSets](../../framework/data/adonet/querying-typed-datasets.md)」(型指定された DataSet のクエリ) を参照してください。 LINQ の使用に関する一般的な情報については、「[統合言語クエリ (LINQ) - C#](../../csharp/programming-guide/concepts/linq/index.md)」または「[統合言語クエリ (LINQ) - Visual Basic](../../visual-basic/programming-guide/concepts/linq/index.md)」を参照してください。|
|**/f\[ields\]**|プロパティの代わりにフィールドを生成します。 既定では、プロパティが生成されます。|
|**/l\[anguage\]:** _language_|使用するプログラミング言語を指定します。 `CS` (C#、既定値)、`VB` (Visual Basic)、`JS` (JScript)、または `VJS` (Visual J#) から選択します。 <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> を実装するクラスの完全修飾名を指定することもできます。|
|**/n\[amespace\]:** _namespace_|生成する型のランタイム名前空間を指定します。 既定の名前空間は `Schemas` です。|
|**/nologo**|バナーを表示しません。|
|**/order**|すべてのパーティクル メンバーに明示的な順序 ID を生成します。|
|**/o\[ut\]:** _directoryName_|ファイルを格納する出力ディレクトリを指定します。 既定値は、現在のディレクトリです。|
|**/u\[ri\]:** _uri_|コードを生成する対象とする、スキーマ内の要素の URI を指定します。 指定した場合、この URI は `/element` オプションで指定したすべての要素に適用されます。|

## <a name="dll-and-exe-file-options"></a>DLL ファイルと EXE ファイルのオプション

|オプション|説明|
|------------|-----------------|
|**/t\[ype\]:** _typename_|スキーマの作成対象とする型の名前を指定します。 複数の型の引数を指定できます。 *typename* によって名前空間が特定されない場合、指定された型を持つアセンブリに含まれるすべての型が対象となります。 *typename* によって名前空間が特定される場合は、その型だけが対象になります。 *typename* の末尾がアスタリスク (\*) の場合は、\* の前にある文字列で始まる型のすべてが対象となります。 `/type` オプションを省略すると、アセンブリに含まれるすべての型についてスキーマが生成されます。|

## <a name="remarks"></a>Remarks

Xsd.exe が実行する操作を次の表に示します。

| | |
|------------|-----------------|
|XDR から XSD へ|XML-Data-Reduced スキーマ ファイルから XML スキーマを生成します。 XDR は初期の XML ベースのスキーマ形式です。|
|XML から XSD へ|XML ファイルから XML スキーマを生成します。|
|XSD から DataSet へ|XSD スキーマ ファイルから共通言語ランタイムの <xref:System.Data.DataSet> クラスを生成します。 生成されるクラスには、標準の XML データ用のリッチ オブジェクト モデルが用意されています。|
|XSD からクラスへ|XSD スキーマ ファイルからランタイム クラスを生成します。 生成されたクラスを <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> と組み合わせて使用すると、このスキーマに従う XML コードの読み書きを実行できます。|
|クラスから XSD へ| ランタイム アセンブリ ファイルに含まれる 1 つ以上の型から XML スキーマを生成します。 生成されたスキーマは、<xref:System.Xml.Serialization.XmlSerializer> で使用される XML 形式を定義します。|

 Xsd.exe によって操作できるのは、W3C (World Wide Web Consortium) が提唱する XSD (XML スキーマ定義) に準拠した XML スキーマだけです。 XML スキーマ定義の提唱や XML 標準の詳細については、<https://w3.org> を参照してください。

## <a name="setting-options-with-an-xml-file"></a>XML ファイルによるオプションの設定

`/parameters` スイッチを使用すると、各種のオプションを設定する単一の XML ファイルを指定できます。 設定できるオプションは、XSD.exe ツールの使用方法によって異なります。 選択肢には、スキーマの生成、コード ファイルの生成、または `DataSet` 機能を含むコード ファイルの生成があります。 たとえば、コード ファイルではなくスキーマを生成する場合、実行可能ファイル (.exe) またはタイプ ライブラリ (.dll) ファイルの名前に `<assembly>` 要素を設定できます。 次の XML に、指定された実行可能ファイルで `<generateSchemas>` 要素を使用する方法を示します。

```xml
<!-- This is in a file named GenerateSchemas.xml. -->
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateSchemas>
   <assembly>ConsoleApplication1.exe</assembly>
</generateSchemas>
</xsd>
```

この XML が GenerateSchemas.xml というファイルに含まれる場合、コマンド プロンプトで、`/parameters` スイッチを使用して次のように入力し、**Enter** キーを押します。

```console
 xsd /p:GenerateSchemas.xml
```

アセンブリにある単一の型のスキーマを生成する場合は、次のような XML を使用します。

```xml
<!-- This is in a file named GenerateSchemaFromType.xml. -->
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateSchemas>
   <type>IDItems</type>
</generateSchemas>
</xsd>
```

しかし、上のコードを使用するには、コマンド プロンプトでアセンブリの名前も指定する必要があります。 コマンド プロンプトで次のように入力します (XML ファイルの名前を GenerateSchemaFromType.xml と仮定します)。

```console
xsd /p:GenerateSchemaFromType.xml ConsoleApplication1.exe
```

`<generateSchemas>` 要素に対しては、次のオプションのうち 1 つだけを指定する必要があります。

|要素|説明|
|-------------|-----------------|
|\<assembly>|スキーマを生成するアセンブリを指定します。|
|\<type>|スキーマを生成するアセンブリに含まれる型を指定します。|
|\<xml>|スキーマを生成する XML ファイルを指定します。|
|\<xdr>|スキーマを生成する XDR ファイルを指定します。|

コード ファイルを生成するには、`<generateClasses>` 要素を使用します。 コード ファイルを生成する例を次に示します。 この例では、生成されるファイルのプログラミング言語と名前空間を設定するための 2 つの属性も示されています。

```xml
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateClasses language='VB' namespace='Microsoft.Serialization.Examples'/>
</xsd>
<!-- You must supply an .xsd file when typing in the command line.-->
<!-- For example: xsd /p:genClasses mySchema.xsd -->
```

 `<generateClasses>` 要素に設定できるオプションは次のとおりです。

|要素|説明|
|-------------|-----------------|
|\<element>|コードを生成する対象となる .xsd ファイルの要素を指定します。|
|\<schemaImporterExtensions>|<xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> クラスから派生する型を指定します。|
|\<schema>|コードを生成する XML スキーマ ファイルを指定します。 複数の \<schema> 要素を使用して、複数の XML スキーマ ファイルを指定できます。|

次の表に、`<generateClasses>` 要素と共に使用するその他の属性を示します。

|属性|説明|
|---------------|-----------------|
|language|使用するプログラミング言語を指定します。 `CS` (C#、既定値)、`VB` (Visual Basic)、`JS` (JScript)、または `VJS` (Visual J#) から選択します。 <xref:System.CodeDom.Compiler.CodeDomProvider> を実装するクラスの完全修飾名を指定することもできます。|
|namespace|生成するコードの名前空間を指定します。 名前空間は、スペースやバックスラッシュ文字を使用しないなどの CLR 標準に準拠する必要があります。|
|options|`none`、`properties` (パブリック フィールドの代わりにプロパティを生成)、`order`、または `enableDataBinding` (前の「XSD ファイルのオプション」セクションの `/order` と `/enableDataBinding` スイッチを参照) のいずれかの値です。|

 `DataSet` 要素を使用すると、`<generateDataSet>` コードを生成する方法を制御できます。 次の XML は、生成されたコードが `DataSet` 構造体 (<xref:System.Data.DataTable> クラスなど) を使用して指定された要素のための Visual Basic コードを作成するように指定します。 生成された DataSet 構造体では LINQ クエリがサポートされます。

 ```xml
 <xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
     <generateDataSet language='VB' namespace='Microsoft.Serialization.Examples' enableLinqDataSet='true'>
     </generateDataSet>
 </xsd>
```

`<generateDataSet>` 要素に設定できるオプションは次のとおりです。

|要素|説明|
|-------------|-----------------|
|\<schema>|コードを生成する XML スキーマ ファイルを指定します。 複数の \<schema> 要素を使用して、複数の XML スキーマ ファイルを指定できます。|

 `<generateDataSet>` 要素と共に使用できる属性を次の表に示します。

|属性|説明|
|---------------|-----------------|
|enableLinqDataSet|LINQ to DataSet を使用して、生成された DataSet を照会できるように指定します。 既定値は false です。|
|language|使用するプログラミング言語を指定します。 `CS` (C#、既定値)、`VB` (Visual Basic)、`JS` (JScript)、または `VJS` (Visual J#) から選択します。 <xref:System.CodeDom.Compiler.CodeDomProvider> を実装するクラスの完全修飾名を指定することもできます。|
|namespace|生成するコードの名前空間を指定します。 名前空間は、スペースやバックスラッシュ文字を使用しないなどの CLR 標準に準拠する必要があります。|

 トップ レベルの `<xsd>` 要素に設定できる属性があります。 これらのオプションは、`<generateSchemas>`、`<generateClasses>`、または `<generateDataSet>` の各子要素と共に使用できます。 次の XML コードは、"MyOutputDirectory" という出力ディレクトリの "IDItems" という要素のコードを生成します。

```xml
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/' output='MyOutputDirectory'>
<generateClasses>
    <element>IDItems</element>
</generateClasses>
</xsd>
```

次の表に、`<xsd>` 要素と共に使用するその他の属性を示します。

|属性|説明|
|---------------|-----------------|
|出力|生成されたスキーマまたはコード ファイルが格納されるディレクトリの名前です。|
|nologo|バナーを表示しません。 `true` または `false` に設定します。|
|help|このツールのコマンド構文とオプションを表示します。 `true` または `false` に設定します。|

## <a name="examples"></a>使用例
 `myFile.xdr` から XML スキーマを生成し、現在のディレクトリに保存するコマンドを次に示します。

```console
xsd myFile.xdr
```

`myFile.xml` から XML スキーマを生成し、指定したディレクトリに保存するコマンドを次に示します。

```console
xsd myFile.xml /outputdir:myOutputDir
```

指定したスキーマと対応するデータセットを C# 言語で生成し、現在のディレクトリ内に `XSDSchemaFile.cs` として保存するコマンドを次に示します。

```console
xsd /dataset /language:CS XSDSchemaFile.xsd
```

`myAssembly.dll` アセンブリ内のすべての型について XML スキーマを生成し、それらを `schema0.xsd` として現在のディレクトリ内に保存するコマンドを次に示します。

```console
xsd myAssembly.dll
```

## <a name="see-also"></a>関連項目

- <xref:System.Data.DataSet>
- <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
- [ツール](../../framework/tools/index.md)
- [Visual Studio 用開発者コマンド プロンプト](../../framework/tools/developer-command-prompt-for-vs.md)
- [LINQ to DataSet の概要](../../framework/data/adonet/linq-to-dataset-overview.md)
- [型指定された DataSet のクエリ](../../framework/data/adonet/querying-typed-datasets.md)
- [統合言語クエリ (LINQ) (C#)](../../csharp/programming-guide/concepts/linq/index.md)
- [統合言語クエリ (LINQ) (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/index.md)
