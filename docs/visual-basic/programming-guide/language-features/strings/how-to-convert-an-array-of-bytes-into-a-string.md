---
title: '方法: バイトの配列を文字列に変換する'
ms.date: 07/20/2015
helpviewer_keywords:
- string conversion [Visual Basic], arrays
- byte arrays [Visual Basic], converting to strings
- examples [Visual Basic], strings
- arrays [Visual Basic], converting to strings
ms.assetid: d0dc8317-9ab3-4324-99f7-3f5788c0e72a
ms.openlocfilehash: 6dbbaafedeca4d2cea625a300d764f61bb575750
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410620"
---
# <a name="how-to-convert-an-array-of-bytes-into-a-string-in-visual-basic"></a>方法: Visual Basic でバイトの配列を文字列に変換する
このトピックでは、バイト配列のバイトを文字列に変換する方法について説明します。  
  
## <a name="example"></a>例  
 この例では、<xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> エンコーディング クラスの <xref:System.Text.Encoding.GetString%2A> メソッドを使用して、バイト配列のすべてのバイトを文字列に変換します。  
  
 [!code-vb[VbVbalrStrings#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#72)]  
  
 バイト配列を文字列に変換するときは、いくつかのエンコード オプションから選択できます。  
  
- <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType>:ASCII (7 ビット) 文字セットのエンコーディングを取得します。  
  
- <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=nameWithType>:ビッグ エンディアン バイト順を使用する UTF-16 形式のエンコードを取得します。  
  
- <xref:System.Text.Encoding.Default%2A?displayProperty=nameWithType>:システムの現在の ANSI コード ページのエンコードを取得します。  
  
- <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType>:リトル エンディアン バイト順を使用する UTF-16 形式のエンコードを取得します。  
  
- <xref:System.Text.Encoding.UTF32%2A?displayProperty=nameWithType>:リトル エンディアン バイト順を使用する UTF-32 形式のエンコードを取得します。  
  
- <xref:System.Text.Encoding.UTF7%2A?displayProperty=nameWithType>:UTF-7 形式のエンコーディングを取得します。  
  
- <xref:System.Text.Encoding.UTF8%2A?displayProperty=nameWithType>:UTF-8 形式のエンコーディングを取得します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Text.Encoding?displayProperty=nameWithType>
- <xref:System.Text.Encoding.GetString%2A>
- [方法: Visual Basic で文字列をバイトの配列に変換する](how-to-convert-strings-into-an-array-of-bytes.md)
