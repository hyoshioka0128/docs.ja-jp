---
title: EDM ジェネレーター (EdmGen.exe)
ms.date: 03/30/2017
ms.assetid: fe8297a1-1fc3-48ce-8eeb-f70f63f857aa
ms.openlocfilehash: 858525a81e7779e7631ee8ac959110ba946cf652
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738535"
---
# <a name="edm-generator-edmgenexe"></a>EDM ジェネレーター (EdmGen.exe)

EdmGen.exe は、Entity Framework モデルとマッピング ファイルを操作するためのコマンドライン ツールです。 EdmGen.exe ツールを使用すると、次の操作を行うことができます。

- データ ソース固有の .NET Framework データ プロバイダーを使用してデータ ソースに接続し、Entity Framework で使用される概念モデル (.csdl)、ストレージ モデル (.ssdl)、およびマッピング (.msl) のファイルを生成する。 詳細については、[EdmGen.exe を使用してモデル ファイルとマッピング ファイルを生成する](how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)」を参照してください。

- 既存のモデルを検証する。 詳細については、[EdmGen.exe を使用してモデル ファイルとマッピング ファイルを検証する](how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)」を参照してください。

- 概念モデル (.csdl) ファイルから生成されたオブジェクト クラスを含む C# コード ファイルまたは Visual Basic コード ファイルを生成する。 詳細については、[EdmGen.exe を使用してオブジェクトレイヤー コードを生成する](how-to-use-edmgen-exe-to-generate-object-layer-code.md)」を参照してください。

- 事前に生成した既存のモデルのビューを含む C# コード ファイルまたは Visual Basic コード ファイルを生成する。 詳細については、「[ビューを事前に生成してクエリ パフォーマンスを向上させる](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))」を参照してください。

EdmGen.exe ツールは、.NET Framework のディレクトリにインストールされます。 多くの場合、C:\windows\Microsoft.NET\Framework\v4.0 にあります。 64 ビット システムの場合は、C:\windows\Microsoft.NET\Framework64\v4.0 にあります。 Visual Studio のコマンド プロンプトから EdmGen.exe ツールにアクセスすることもできます ( **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft Visual Studio 2010]** 、 **[Visual Studio Tools]** の順にポイントして、 **[Visual Studio 2010 コマンド プロンプト]** をクリックします)。

## <a name="syntax"></a>構文

```console
EdmGen /mode:choice [options]
```

## <a name="mode"></a>モード

EdmGen.exe ツールを使用する場合、次のいずれかのモードを指定する必要があります。

|モード|説明|
|----------|-----------------|
|`/mode:ValidateArtifacts`|.csdl、.ssdl、および .msl ファイルを検証し、エラーまたは警告を表示します。<br /><br /> このオプションを使用するには、少なくとも `/inssdl` 引数または `/incsdl` 引数のどちらかが必要です。 `/inmsl` を指定する場合は、`/inssdl` 引数と `/incsdl` 引数も必要です。|
|`/mode:FullGeneration`|`/connectionstring` オプションで指定されたデータベース接続情報を使用し、.csdl、.ssdl、.msl、オブジェクト レイヤー、およびビュー ファイルを生成します。<br /><br /> このオプションを使用するには、`/connectionstring` 引数に加え、`/project` 引数を指定するか、`/outssdl`、`/outcsdl`、`/outmsdl`、`/outobjectlayer`、`/outviews`、`/namespace`、`/entitycontainer` の各引数を指定する必要があります。|
|`/mode:FromSSDLGeneration`|指定された .ssdl ファイルから、.csdl ファイル、.msl ファイル、ソース コード、およびビューを生成します。<br /><br /> このオプションを使用するには、`/inssdl` 引数に加え、`/project` 引数を指定するか、`/outcsdl`、`/outmsl`、`/outobjectlayer`、`/outviews`、`/namespace,`、`/entitycontainer` の各引数を指定する必要があります。|
|`/mode:EntityClassGeneration`|.csdl ファイルから生成されたクラスを含むソース コード ファイルを作成します。<br /><br /> このオプションを使用するには、`/incsdl` 引数に加え、`/project` 引数または `/outobjectlayer` 引数のどちらかを指定する必要があります。 `/language` 引数は省略可能です。|
|`/mode:ViewGeneration`|.csdl、.ssdl、および .msl ファイルから生成されたビューを含むソース コード ファイルを作成します。<br /><br /> このオプションを使用するには、`/inssdl`、`/incsdl`、`/inmsl,` の各引数に加え、`/project` 引数または `/outviews` 引数のどちらかを指定する必要があります。 `/language` 引数は省略可能です。|

## <a name="options"></a>オプション

|オプション|説明|
|------------|-----------------|
|`/p[roject]:`\<string>|使用するプロジェクト名を指定します。 このプロジェクト名は、名前空間の設定の既定値、モデル ファイルとマッピング ファイルの名前、オブジェクト ソース ファイルの名前、およびビュー生成のソース ファイルの名前として使用されます。 エンティティのコンテナー名が \<project>Context に設定されています。|
|`/prov[ider]:`\<string>|ストレージ モデル (.ssdl) ファイルの生成に使用する .NET Framework データ プロバイダーの名前です。 既定のプロバイダーは .NET Framework SQL Server 用データ プロバイダー (<xref:System.Data.SqlClient?displayProperty=nameWithType>) です。|
|`/c[onnectionstring]:`\<connection string>|データ ソースへの接続に使用する文字列を指定します。|
|`/incsdl:`\<file>|.csdl ファイル、または .csdl ファイルがあるディレクトリを指定します。 この引数は複数回指定できるので、複数のディレクトリまたは .csdl ファイルを指定できます。 概念モデルが複数のファイルに分割されている場合にクラスの生成 (`/mode:EntityClassGeneration`) またはビューの生成 (`/mode:ViewGeneration`) を行うときは、複数のディレクトリを指定すると便利です。 また、複数のモデルを検証する (`/mode:ValidateArtifacts`) 場合にも役立ちます。|
|`/refcsdl:`\<file>|追加の .csdl ファイル、またはソース .csdl ファイルの参照の解決に使用するファイルを指定します  (ソース .csdl ファイルは、`/incsdl` オプションで指定したファイルです)。 `/refcsdl` ファイルには、ソース .csdl ファイルが依存する型が含まれています。 この引数は複数回指定できます。|
|`/inmsl:`\<file>|.msl ファイル、または .msl ファイルがあるディレクトリを指定します。 この引数は複数回指定できるので、複数のディレクトリまたは .msl ファイルを指定できます。 概念モデルが複数のファイルに分割されている場合にビューを生成 (`/mode:ViewGeneration`) するときは、複数のディレクトリを指定すると便利です。 また、複数のモデルを検証する (`/mode:ValidateArtifacts`) 場合にも役立ちます。|
|`/inssdl:`\<file>|.ssdl ファイル、または .ssdl ファイルがあるディレクトリを指定します。 この引数は複数回指定できるので、複数のディレクトリまたは .ssdl ファイルを指定できます。 これは、複数のモデルを検証する場合 `(/mode:ValidateArtifacts)` に役立ちます。|
|`/outcsdl:`\<file>|作成される .csdl ファイルの名前を指定します。|
|`/outmsl:`\<file>|作成される .msl ファイルの名前を指定します。|
|`/outssdl:`\<file>|作成される .ssdl ファイルの名前を指定します。|
|`/outobjectlayer:`\<file>|.csdl ファイルから生成されたオブジェクトを含むソース コード ファイルの名前を指定します。|
|`/outviews:`\<file>|生成されたビューを含むソース コード ファイルの名前を指定します。|
|`/language:`[VB&#124;CSharp]|生成されるソース コード ファイルの言語を指定します。 既定の言語は C# です。|
|`/namespace:`\<string>|使用するモデル名前空間を指定します。 名前空間は、`/mode:FullGeneration` または `/mode:FromSSDLGeneration` の実行時に .csdl ファイルに設定されます。 `/mode:EntityClassGeneration` の実行時には名前空間は使用されません。|
|`/entitycontainer:`\<string>|生成されたモデル ファイルとマッピング ファイルの `<EntityContainer>` 要素に適用する名前を指定します。|
|`/pl[uralize]`|単数形と複数形の英語のルールを、概念モデルの `Entity`、`EntitySet`、および `NavigationProperty` の各名前に適用します。 このオプションでは、以下の処理が実行されます。<br /><br /> - すべての `EntityType` 名を単数形にします。<br />- すべての `EntitySet` 名を複数形にします。<br />- 最大で 1 つのエンティティを返す各 `NavigationProperty` について、名前を単数形にします。<br />- 複数のエンティティを返す各 `NavigationProperty` について、名前を複数形にします。|
|`/SuppressForeignKeyProperties or /nofk`|外部キー列が概念モデルのエンティティ型のスカラー プロパティとして公開されないようにします。|
|`/help` または `?`|このツールのコマンド構文とオプションを表示します。|
|`/nologo`|著作権メッセージが表示されないようにします。|
|`/targetversion:` \<string>|生成されたコードのコンパイルに使用される .NET Framework のバージョンです。 サポートされているバージョンは 4 と 4.5 です。 既定値は 4 です。|

## <a name="in-this-section"></a>このセクションの内容

[方法: EdmGen.exe を使用してモデル ファイルとマッピング ファイルを生成する](how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)

[方法: EdmGen.exe を使用してオブジェクトレイヤー コードを生成する](how-to-use-edmgen-exe-to-generate-object-layer-code.md)

[方法: EdmGen.exe を使用してモデル ファイルとマッピング ファイルを検証する](how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)

## <a name="see-also"></a>関連項目

- [ADO.NET Entity Data Model ツール](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [Entity Data Model](../entity-data-model.md)
- [CSDL、SSDL、および MSL 仕様](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
