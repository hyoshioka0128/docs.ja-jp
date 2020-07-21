---
title: ソースとなる Office Open XML ドキュメントの作成
ms.date: 07/20/2015
ms.assetid: 61ccd6fb-0c47-4075-afdf-5b5021330f21
ms.openlocfilehash: 9f44c8d0f4080224c461736fdbdf3acd854e4a89
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410839"
---
# <a name="creating-the-source-office-open-xml-document-visual-basic"></a>ソースとなる Office Open XML ドキュメントの作成 (Visual Basic)
このトピックでは、このチュートリアルの他の例で使用する Office Open XML WordprocessingML ドキュメントを作成する方法について説明します。 この手順に従うと、それぞれの例に記載されているとおりの出力が得られます。  
  
 ただし、このチュートリアルの例では、任意の有効な WordprocessingML ドキュメントを使用できます。  
  
 このチュートリアルで使用するドキュメントを作成するには、Microsoft Office 2007 以降がインストールされているか、Microsoft Office 2003 と Word/Excel/PowerPoint 2007 ファイル形式用 Microsoft Office 互換機能パックを所有している必要があります。  
  
## <a name="creating-the-wordprocessingml-document"></a>WordprocessingML ドキュメントの作成  
  
#### <a name="to-create-the-wordprocessingml-document"></a>WordprocessingML ドキュメントを作成するには  
  
1. 新しい Microsoft Word 文書を作成します。  
  
2. 新しい文書に次のテキストを貼り付けます。  
  
    ```text  
    Parsing WordprocessingML with LINQ to XML  
  
    The following example prints to the console.  
  
    Imports System  
  
    Class Program  
        Public Shared  Sub Main(ByVal args() As String)  
            Console.WriteLine("Hello World")  
        End Sub  
    End Class  
  
    This example produces the following output:  
  
    Hello World  
    ```  
  
3. "見出し 1" スタイルを使用して最初の行を書式設定します。  
  
4. Visual Basic コードを含む行を選択します。 最初の行は `Imports` キーワードで始まります。 最後の行は "End Class" です。 クーリエ フォントを使用してこれらの行を書式設定します。 これらの行を新しいスタイルで書式設定し、このスタイルに "Code" という名前を付けます。  
  
5. 最後に、出力が含まれる行全体を選択し、`Code` スタイルを使用して書式設定します。  
  
6. ドキュメントを保存し、SampleDoc.docx という名前を付けます。  
  
    > [!NOTE]
    > Microsoft Word 2003 を使用している場合、 **[ファイルの種類]** ボックスの一覧の **[Word 2007 文書]** をクリックします。  
  
## <a name="see-also"></a>関連項目

- [チュートリアル: WordprocessingML ドキュメント内のコンテンツの操作 (Visual Basic)](tutorial-manipulating-content-in-a-wordprocessingml-document.md)
