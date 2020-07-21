---
title: '方法: ファイルのテキストの読み取り'
description: この記事では、.NET デスクトップ アプリの StreamReader クラスを使用して、テキスト ファイルから同期または非同期でテキストを読み取る方法の例を示します。
ms.date: 01/03/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, reading text from files
- reading text files
- reading data, text files
- data streams, reading text from files
- I/O [.NET Framework], reading text from files
ms.assetid: ed180baa-dfc6-4c69-a725-46e87edafb27
ms.openlocfilehash: cbdeab3e907b34b6658eef7228fa6567ae198b08
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84447057"
---
# <a name="how-to-read-text-from-a-file"></a>方法: ファイルのテキストの読み取り
次に、.NET デスクトップ アプリを使用してテキスト ファイルから同期でテキストを読み取る方法と非同期でテキストを読み取る方法の例を示します。 どちらの例でも、<xref:System.IO.StreamReader> クラスのインスタンスを作成する場合に、ファイルの相対パスまたは絶対パスを指定します。
  
> [!NOTE]
> Windows ランタイムではファイルに対する読み取りと書き込みに別のストリーム型が用意されているため、これらのコード例はユニバーサル Windows プラットフォーム (UWP) アプリの開発には適用されません。 UWP アプリのファイルからテキストを読み取る方法を示す例については、「[Quickstart: Reading and writing files](https://docs.microsoft.com/previous-versions/windows/apps/hh758325(v=win.10))」 (クイック スタート: ファイルの読み取りと書き込み) を参照してください。 .NET Framework ストリームと Windows ランタイム ストリーム間で変換を行う方法を示す例については、「[方法: .NET Framework ストリームと Windows ランタイム ストリームの間で変換を行う](how-to-convert-between-dotnet-streams-and-winrt-streams.md)」を参照してください。  
  
## <a name="example-synchronous-read-in-a-console-app"></a>例:コンソール アプリの同期読み取り  
次の例では、コンソール アプリ内での同期読み取り操作を示します。 この例では、ストリーム リーダーを使用してテキスト ファイルを開き、コンテンツが文字列にコピーされ、文字列がコンソールに出力されます。  
  
> [!IMPORTANT]
> サンプルでは、*TestFile.txt* という名前のファイルがアプリと同じフォルダーに入っていると想定しています。  

 [!code-csharp[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source3.cs#3)]
 [!code-vb[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source3.vb#3)]  
  
## <a name="example-asynchronous-read-in-a-wpf-app"></a>例:WPF アプリの非同期読み取り
 次の例では、Windows Presentation Foundation (WPF) アプリ内での非同期読み取り操作を示します。  
  
> [!IMPORTANT]
> サンプルでは、*TestFile.txt* という名前のファイルがアプリと同じフォルダーに入っていると想定しています。  

 [!code-csharp[TextFiles](../../../samples/snippets/csharp/VS_Snippets_Wpf/TextFiles/MainWindow.xaml.cs)]
 [!code-vb[TextFiles](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextFiles/MainWindow.xaml.vb)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.IO.StreamReader>  
- <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- [非同期ファイル I/O](asynchronous-file-i-o.md)  
- [方法: ディレクトリ一覧を作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))  
- [クイック スタート:ファイルの読み書き](https://docs.microsoft.com/previous-versions/windows/apps/hh758325%28v=win.10%29)  
- [方法: .NET Framework ストリームと Windows ランタイム ストリームの間で変換を行う](how-to-convert-between-dotnet-streams-and-winrt-streams.md)  
- [方法: 新しく作成されたデータ ファイルに対して読み書きする](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [方法: ログ ファイルを開いて情報を追加する](how-to-open-and-append-to-a-log-file.md)  
- [方法: テキストのファイルへの書き込み](how-to-write-text-to-a-file.md)  
- [方法: 文字列からの文字の読み取り](how-to-read-characters-from-a-string.md)  
- [方法: 文字列への文字の書き込み](how-to-write-characters-to-a-string.md)  
- [ファイルおよびストリーム入出力](index.md)
