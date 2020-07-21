---
title: '方法: ファイルを圧縮して抽出する'
description: System.IO.Compression を使用してファイルを圧縮して抽出します。 ZipFile、ZipArchive、ZipArchiveEntry、DeflateStream、GZipStream の使用例を参照します。
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET Framework], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
ms.openlocfilehash: c13f464432aa6f67136d3a844bdeda256e7ab9b6
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769237"
---
# <a name="how-to-compress-and-extract-files"></a>方法: ファイルを圧縮して抽出する

<xref:System.IO.Compression> 名前空間には、ファイルおよびストリームを圧縮および展開するための次の型が含まれています。 これらの型を使用して、圧縮ファイルの内容を読み取り、変更することもできます。

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

圧縮ファイルで実行できる操作の例を次に示します。 これらの例では、プロジェクトに次の NuGet パッケージを追加する必要があります。

- [System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)
- [System.IO.Compression.ZipFile](https://www.nuget.org/packages/System.IO.Compression.ZipFile)

.NET Framework を使用している場合は、プロジェクトにこれら 2 つのライブラリへの参照を追加します。

- `System.IO.Compression`
- `System.IO.Compression.FileSystem`

## <a name="example-1-create-and-extract-a-zip-file"></a>例 1: .zip ファイルを作成して抽出する

次の例では、<xref:System.IO.Compression.ZipFile> クラスを使用して圧縮された *.zip* ファイルの作成と抽出を行う方法を示しています。 この例では、フォルダーの内容を新しい *.zip* ファイルに圧縮し、その zip を新しいフォルダーに抽出します。

サンプルを実行するには、プログラムのフォルダーに *start* フォルダーを作成し、圧縮するファイルをそこに置きます。

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a>例 2:特定の拡張子のファイルを抽出する

次の例では、既存の *.zip* ファイルの内容を反復処理し、拡張子が *.txt* のファイルを抽出します。 <xref:System.IO.Compression.ZipArchive> クラスを使用して zip にアクセスし、<xref:System.IO.Compression.ZipArchiveEntry> クラスを使用して個々のエントリを調べます。 <xref:System.IO.Compression.ZipArchiveEntry> オブジェクトの拡張メソッド <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> は、<xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType> クラスで使用できます。

サンプルを実行するには、*result.zip* という名前の *.zip* ファイルをプログラム フォルダーに配置します。 入力を求められたら、抽出先のフォルダー名を指定します。

> [!IMPORTANT]
> ファイルを解凍する場合は、解凍先のディレクトリを回避する悪意のあるファイル パスを検索する必要があります。 これは、パス トラバーサル攻撃と呼ばれます。 次の例では、悪意のあるファイル パスを確認して安全な解凍手段を提供する方法を示します。

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a>例 3:既存の zip にファイルを追加する

次の例では、<xref:System.IO.Compression.ZipArchive> クラスを使用して既存の *.zip* ファイルにアクセスし、ファイルを追加します。 新しいファイルは、既存の zip に追加するときに圧縮されます。

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a>例 4:.gz ファイルを圧縮および展開する

また、<xref:System.IO.Compression.GZipStream> クラスと <xref:System.IO.Compression.DeflateStream> クラスを使用してデータを圧縮および展開することもできます。 圧縮と展開には同じ圧縮アルゴリズムが使用されます。 多くの一般的なツールを使用して、 *.gz* ファイルに書き込まれた <xref:System.IO.Compression.GZipStream> オブジェクトを展開できます。 次の例では、<xref:System.IO.Compression.GZipStream> クラスを使用してファイルのディレクトリを圧縮および展開する方法を示します。

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a>関連項目

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [ファイルおよびストリーム入出力](index.md)
