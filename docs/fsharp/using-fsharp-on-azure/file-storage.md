---
title: F# を使用した Azure File Storage の概要
description: Azure File Storage を使用してクラウドにファイル データを格納し、Azure 仮想マシン (VM) から、または Windows を実行しているオンプレミスのアプリケーションからクラウド ファイル共有をマウントします。
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: 1b38ee53f2f73f7b7f4ee12f712f487cb726d41e
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739593"
---
# <a name="get-started-with-azure-file-storage-using-f"></a>F を使用して Azure ファイル ストレージを使用する\#

Azure File Storage は、標準の [サーバー メッセージ ブロック (SMB) プロトコル](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)を使用してクラウドでファイル共有を提供するサービスです。 SMB 2.1 と SMB 3.0 の両方がサポートされます。 Azure File Storage を使用すると、コストがかかる書き換えを行わずに、ファイル共有に依存しているレガシ アプリケーションをすばやく Azure に移行することができます。 Azure 仮想マシンまたはクラウド サービスで実行されているアプリケーション、またはオンプレミスのクライアントから実行されているアプリケーションは、デスクトップ アプリケーションが一般的な SMB 共有をマウントするのと同じように、クラウドにファイル共有をマウントできます。 このため、任意の数のアプリケーション コンポーネントが、File Storage 共有をマウントして同時にアクセスできます。

ファイル記憶域の概念の概要については[、.NET のファイル記憶域のガイドを](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files)参照してください。

## <a name="prerequisites"></a>前提条件

このガイドを使用するには、まず[Azure ストレージ アカウントを作成する](https://docs.microsoft.com/azure/storage/storage-create-storage-account)必要があります。
このアカウントにはストレージアクセスキーも必要です。

## <a name="create-an-f-script-and-start-f-interactive"></a>F# スクリプトを作成し、F# 対話を開始する

この記事のサンプルは、F# アプリケーションまたは F# スクリプトで使用できます。 F# スクリプトを作成するには、F# 開発環境`.fsx`で拡張子を`files.fsx`持つファイルを作成します。

次に、パッケージ[マネージャー](package-management.md)を使用して[Paket](https://fsprojects.github.io/Paket/)や[NuGet](https://www.nuget.org/)ディレクティブを`WindowsAzure.Storage`使用してスクリプトでパッケージと参照`WindowsAzure.Storage.dll`を`#r`インストールします。

### <a name="add-namespace-declarations"></a>名前空間宣言の追加

次の `open` ステートメントを `files.fsx` ファイルの先頭に追加します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>接続文字列を取得する

このチュートリアルには、Azure ストレージ接続文字列が必要です。 接続文字列の詳細については、「 ストレージ接続文字列[の構成](https://docs.microsoft.com/azure/storage/storage-configure-connection-string)」を参照してください。

このチュートリアルでは、次のように、スクリプトに接続文字列を入力します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L11-L11)]

ただし、実際のプロジェクト**では推奨されません**。 ストレージ アカウント キーは、ストレージ アカウントの root パスワードに似ています。 ストレージ アカウント キーは常に慎重に保護してください。 このキーを他のユーザーに配布したり、ハードコーディングしたり、他のユーザーがアクセスできるプレーン テキスト ファイルに保存したりしないでください。 キーが侵害されたと思われる場合は、Azure ポータルを使用してキーを再生成できます。

実際のアプリケーションでは、ストレージ接続文字列を維持する最善の方法は、構成ファイルです。 構成ファイルから接続文字列を取得するには、次の操作を行います。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L13-L15)]

Azure Configuration Manager の使用はオプションです。 .NET Framework の`ConfigurationManager`型などの API を使用することもできます。

### <a name="parse-the-connection-string"></a>接続文字列を解析する

接続文字列を解析するには、次のコマンドを使用します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L21-L22)]

これにより、 が`CloudStorageAccount`返されます。

### <a name="create-the-file-service-client"></a>ファイル サービス クライアントを作成する

この`CloudFileClient`型を使用すると、ファイル ストレージに格納されているファイルをプログラムで使用できます。 サービス クライアントを作成する方法の 1 つを次に示します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L28-L28)]

これで、データをファイル ストレージから読み取り、ファイル ストレージに書き込むコードを記述する準備ができました。

## <a name="create-a-file-share"></a>ファイル共有を作成する

次に、ファイル共有がまだ存在しない場合に作成する例を示します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L34-L35)]

## <a name="create-a-root-directory-and-a-subdirectory"></a>ルート ディレクトリとサブディレクトリを作成する

ここでは、ルートディレクトリを取得し、ルートのサブディレクトリを取得します。 存在しない場合は、両方を作成します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L41-L43)]

## <a name="upload-text-as-a-file"></a>テキストをファイルとしてアップロードする

この例では、テキストをファイルとしてアップロードする方法を示します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L49-L50)]

### <a name="download-a-file-to-a-local-copy-of-the-file"></a>ファイルのローカル コピーにファイルをダウンロードする

ここでは、作成したばかりのファイルをダウンロードして、内容をローカルファイルに追加します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L56-L56)]

### <a name="set-the-maximum-size-for-a-file-share"></a>ファイル共有の最大サイズの設定

次の例では、共有の現在の使用状況を確認する方法と、共有のクォータを設定する方法を示します。 `FetchAttributes`共有`Properties`の を設定し、`SetProperties`ローカルの変更を Azure ファイル ストレージに反映するために呼び出す必要があります。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L62-L72)]

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>ファイルまたはファイル共有の Shared Access Signature の生成

ファイル共有または個々のファイルの Shared Access Signature (SAS) を生成することができます。 また、ファイル共有に共有アクセス ポリシーを作成して、Shared Access Signature を管理することもできます。 共有アクセス ポリシーを作成することをお勧めします。これにより、侵害されそうな場合に SAS を取り消すことができます。

ここでは、共有に共有アクセス ポリシーを作成し、そのポリシーを使用して、共有内のファイルに対する SAS の制約を提供します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L78-L94)]

Shared Access Signature の作成と使用の詳細については、「[Shared Access Signature (SAS) の使用](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)」と、[Blob Storage での SAS の作成と使用](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-2)に関するページを参照してください。

### <a name="copy-files"></a>ファイルのコピー

ファイルを別のファイル、BLOB、または BLOB にファイルにコピーできます。 BLOB をファイルにコピーする場合、またはファイルを BLOB にコピーする場合は、同じストレージ アカウント内でコピーする場合でも、共有アクセス署名 (SAS) を使用してソース オブジェクトを認証する*必要があります*。

### <a name="copy-a-file-to-another-file"></a>別のファイルへのファイルのコピー

ここでは、同じ共有内の別のファイルにファイルをコピーします。 このコピー操作では同じストレージ アカウント内のファイルがコピーされるため、共有キー認証を使用してコピーを実行できます。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L100-L101)]

### <a name="copy-a-file-to-a-blob"></a>BLOB へのファイルのコピー

ここでは、ファイルを作成し、同じストレージ アカウント内の BLOB にコピーします。 コピー操作中にソース ファイルへのアクセスを認証するためにサービスが使用するソース ファイルの SAS を作成します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L107-L120)]

同じ方法で、ファイルに BLOB をコピーできます。 ソース オブジェクトが BLOB である場合、SAS を作成して、コピー操作中にその BLOB へのアクセスを認証します。

## <a name="troubleshooting-file-storage-using-metrics"></a>メトリックを使用した File Storage のトラブルシューティング

Azure ストレージ分析では、ファイル ストレージのメトリックがサポートされています。 メトリック データを使用すると、要求のトレースや問題の診断ができます。

[Azure ポータル](https://portal.azure.com)からファイル ストレージのメトリックを有効にするか、F# から次のようにすることができます。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L126-L140)]

## <a name="next-steps"></a>次のステップ

Azure ファイル ストレージの詳細については、これらのリンクを参照してください。

### <a name="conceptual-articles-and-videos"></a>概念に関する記事とビデオ

- [Azure File Storage: Windows および Linux 用の円滑なクラウド SMB ファイル システム](https://azure.microsoft.com/resources/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
- [Linux で Azure ファイル ストレージを使用する方法](https://docs.microsoft.com/azure/storage/storage-how-to-use-files-linux)

### <a name="tooling-support-for-file-storage"></a>File Storage 用のツールのサポート

- [Azure Storage での Azure PowerShell の使用](https://docs.microsoft.com/azure/storage/storage-powershell-guide-full)
- [Microsoft Azure Storage で AzCopy を使用する方法](https://docs.microsoft.com/azure/storage/storage-use-azcopy)
- [Azure CLI を使用して BLOB を作成、ダウンロード、一覧表示する](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-cli#create-and-manage-file-shares)

### <a name="reference"></a>リファレンス

- [.NET 用ストレージ クライアント ライブラリ リファレンス](https://msdn.microsoft.com/library/azure/mt347887.aspx)
- [File サービスの REST API リファレンス](/rest/api/storageservices/fileservices/File-Service-REST-API)

### <a name="blog-posts"></a>ブログ記事

- [Azure File Storage の一般提供開始](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
- [Azure ファイル ストレージ内](https://azure.microsoft.com/blog/inside-azure-file-storage/)
- [Microsoft Azure File サービスの概要](https://docs.microsoft.com/archive/blogs/windowsazurestorage/introducing-microsoft-azure-file-service)
- [Microsoft Azure Files への接続の維持](https://docs.microsoft.com/archive/blogs/windowsazurestorage/persisting-connections-to-microsoft-azure-files)
