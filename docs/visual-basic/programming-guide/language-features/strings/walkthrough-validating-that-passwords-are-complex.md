---
title: パスワードの複雑さの検証
ms.date: 07/20/2015
helpviewer_keywords:
- String data type [Visual Basic], validation
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
ms.openlocfilehash: 7b2d6a81f5dc88688a469b96d56a098a2b45c59f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363686"
---
# <a name="walkthrough-validating-that-passwords-are-complex-visual-basic"></a>チュートリアル: パスワードの複雑さの検証 (Visual Basic)
このメソッドでは、強力なパスワードの特性をチェックし、不合格になったチェックに関する情報で文字列パラメーターを更新します。  
  
 セキュリティで保護されたシステムでは、パスワードを使用してユーザーを承認できます。 ただし、パスワードは、承認されていないユーザーが推測するのは難しいものである必要があります。 攻撃者は、辞書 (またはさまざまな言語の複数の辞書) のすべての単語を反復処理する "*辞書攻撃*" プログラムを使用し、単語のいずれかがユーザーのパスワードとして機能するかどうかをテストする可能性があります。 "Yankees" や "Mustang" のような脆弱なパスワードはすぐに推測できます。 "?You'L1N3vaFiNdMeyeP@sSWerd!" のような強力なパスワードは、推測される可能性がはるかに低くなります。 パスワードで保護されたシステムでは、ユーザーが強力なパスワードを選択できるようにする必要があります。  
  
 強力なパスワードは複雑であり (大文字、小文字、数字、特殊文字が混在)、単語ではありません。 次の例は、複雑さを検証する方法を示しています。  
  
## <a name="example"></a>例  
  
### <a name="code"></a>コード  
 [!code-vb[VbVbcnRegEx#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#1)]  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 対象のパスワードを含む文字列を渡して、このメソッドを呼び出します。  
  
 この例で必要な要素は次のとおりです。  
  
- <xref:System.Text.RegularExpressions> 名前空間のメンバーへのアクセス許可。 コード内でメンバー名を完全修飾していない場合は、`Imports` ステートメントを追加します。 詳細については、「[Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)」を参照してください。  
  
## <a name="security"></a>セキュリティ  
 ネットワーク経由でパスワードを移動する場合は、セキュリティで保護された方法でデータを転送する必要があります。 詳細については、「[ASP.NET Web Application Security (ASP.NET Web アプリケーションのセキュリティ)](https://docs.microsoft.com/previous-versions/aspnet/330a99hc(v=vs.100))」をご覧ください。
  
 複雑さのチェックをさらに追加することで、`ValidatePassword` 関数の精度を高めることができます。  
  
- パスワードとその部分文字列を、ユーザーの名前、ユーザー識別子、アプリケーション定義の辞書と比較します。 さらに、比較を行うときに、見た目が似ている文字は同等に扱います。 たとえば、文字 "l"、"e" は数字 "1"、"3" と同等に扱います。  
  
- 大文字が 1 つしかない場合は、パスワードの最初の文字ではないことを確認します。  
  
- パスワードの最後の 2 文字が文字であることを確認します。  
  
- すべての記号がキーボードの上部の行から入力されているパスワードは許可しないでください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Text.RegularExpressions.Regex>
- [ASP.NET Web アプリケーションのセキュリティ](https://docs.microsoft.com/previous-versions/aspnet/330a99hc(v=vs.100))
