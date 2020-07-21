---
title: バイト配列に読み取るにはファイルが大きすぎます。
ms.date: 07/20/2015
ms.assetid: 686630a6-a439-46c7-8d7b-34613ae4c5d8
ms.openlocfilehash: b81fc9332d5f1347404fcdd73bce72b6b09778b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363125"
---
# <a name="file-is-too-large-to-read-into-a-byte-array"></a>バイト配列に読み取るにはファイルが大きすぎます。
バイト配列に読み取ろうとしているファイルのサイズが 4 GB を超えています。 `My.Computer.FileSystem.ReadAllBytes` メソッドは、このサイズを超えるファイルを読み取ることができません。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- <xref:System.IO.StreamReader> を使用してファイルを読み取ります。 詳細については、「[.NET Framework のファイル I/O とファイル システムの基礎 (Visual Basic)](../../developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>
- <xref:System.IO.StreamReader>
- [Visual Basic におけるファイル アクセス](../../developing-apps/programming/drives-directories-files/file-access.md)
- [方法: StreamReader を使用してファイルからテキストを読み取る](../../developing-apps/programming/drives-directories-files/how-to-read-text-from-files-with-a-streamreader.md)
