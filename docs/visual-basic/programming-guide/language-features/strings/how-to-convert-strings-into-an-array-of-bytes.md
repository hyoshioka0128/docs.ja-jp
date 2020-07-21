---
title: '方法: 文字列をバイトの配列に変換する'
ms.date: 07/20/2015
helpviewer_keywords:
- string conversion [Visual Basic], arrays
- arrays [Visual Basic], converting strings to
- byte arrays
- examples [Visual Basic], string conversion
- arrays [Visual Basic], byte arrays
ms.assetid: f477d35c-a3fc-4a30-b1d4-cd0d353aae1d
ms.openlocfilehash: 3ee1d5e1e31054f23f4510c7a112d8e3473bcdd7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410607"
---
# <a name="how-to-convert-strings-into-an-array-of-bytes-in-visual-basic"></a>方法: Visual Basic で文字列をバイトの配列に変換する
このトピックでは、文字列をバイトの配列に変換する方法について説明します。  
  
## <a name="example"></a>例  
 この例では、<xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> エンコーディング クラスの <xref:System.Text.Encoding.GetBytes%2A> メソッドを使用して、文字列をバイトの配列に変換します。  
  
 [!code-vb[VbVbalrStrings#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#74)]  
  
 文字列をバイト配列に変換するときは、いくつかのエンコード オプションから選択できます。  
  
- <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType>:ASCII (7 ビット) 文字セットのエンコーディングを取得します。  
  
- <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=nameWithType>:ビッグ エンディアン バイト順を使用する UTF-16 形式のエンコードを取得します。  
  
- <xref:System.Text.Encoding.Default%2A?displayProperty=nameWithType>:システムの現在の ANSI コード ページのエンコードを取得します。  
  
- <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType>:リトル エンディアン バイト順を使用する UTF-16 形式のエンコードを取得します。  
  
- <xref:System.Text.Encoding.UTF32%2A?displayProperty=nameWithType>:リトル エンディアン バイト順を使用する UTF-32 形式のエンコードを取得します。  
  
- <xref:System.Text.Encoding.UTF7%2A?displayProperty=nameWithType>:UTF-7 形式のエンコーディングを取得します。  
  
- <xref:System.Text.Encoding.UTF8%2A?displayProperty=nameWithType>:UTF-8 形式のエンコーディングを取得します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Text.Encoding?displayProperty=nameWithType>
- <xref:System.Text.Encoding.GetBytes%2A>
- [方法: Visual Basic でバイトの配列を文字列に変換する](how-to-convert-an-array-of-bytes-into-a-string.md)
