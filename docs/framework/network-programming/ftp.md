---
title: FTP - .NET
description: FtpWebRequest と FtpWebResponse クラスを使用することで .NET Framework によって提供される、FTP の包括的なサポートについて学習します。
ms.date: 03/30/2017
helpviewer_keywords:
- FTP
ms.assetid: 9b43f8b4-89d7-46a7-89fc-71aca916dd32
ms.openlocfilehash: d21ca43cd1041df358dc5e2add9560fb33e85d83
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502588"
---
# <a name="ftp"></a>FTP

.NET Framework は、<xref:System.Net.FtpWebRequest> クラスと <xref:System.Net.FtpWebResponse> クラスを使用して、FTP プロトコルの包括的なサポートを提供します。 これらのクラスは <xref:System.Net.WebRequest> と <xref:System.Net.WebResponse> から派生します。 ほとんどの場合、<xref:System.Net.WebRequest> クラスと <xref:System.Net.WebResponse> クラスは、要求を行うために必要なすべてを提供しますが、プロパティとして公開されている FTP 固有の機能にアクセスする必要がある場合は、これらのクラスを <xref:System.Net.FtpWebRequest> または <xref:System.Net.FtpWebResponse> に型キャストすることができます。

## <a name="examples"></a>使用例

詳細については、次のトピックを参照してください。[方法: FTP を使用してファイルをダウンロードする](how-to-download-files-with-ftp.md)、[方法:FTP を使用してファイルをアップロードする](how-to-upload-files-with-ftp.md)、[方法:FTP でディレクトリの内容を一覧表示する](how-to-list-directory-contents-with-ftp.md)。

## <a name="ftp-and-proxies"></a>FTP とプロキシ

(<xref:System.Net.FtpWebRequest.Proxy%2A> プロパティで指定された) プロキシが HTTP プロキシの場合、<xref:System.Net.WebRequestMethods.Ftp.DownloadFile>、<xref:System.Net.WebRequestMethods.Ftp.ListDirectory>、および <xref:System.Net.WebRequestMethods.Ftp.ListDirectoryDetails> コマンドのみがサポートされます。

## <a name="see-also"></a>関連項目

- [プロキシを介したインターネットへのアクセス](accessing-the-internet-through-a-proxy.md)
- [ネットワーク プログラミングのサンプル](network-programming-samples.md)
- [アプリケーション プロトコルの使用](using-application-protocols.md)
