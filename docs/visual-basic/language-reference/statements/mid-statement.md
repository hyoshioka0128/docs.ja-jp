---
title: Mid ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.MidB
- vb.Mid
helpviewer_keywords:
- substrings [Visual Basic], Mid statement
- strings [Visual Basic], substrings
- Mid statement [Visual Basic]
- strings [Visual Basic], replacing
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
ms.openlocfilehash: 90408fd8a8cfc9b74c8422d0571d61f8534403f3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404454"
---
# <a name="mid-statement"></a>Mid ステートメント
`String` 変数内の指定した数の文字を別の文字列の文字に置き換えます。  
  
## <a name="syntax"></a>構文  
  
```vb  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## <a name="parts"></a>指定項目  
 `Target`  
 必須です。 変更する `String` 変数の名前。  
  
 `Start`  
 必須です。 `Integer` 式。 テキストの置換を開始する `Target` の文字の位置。 `Start` は 1 から始まるインデックスを使用します。  
  
 `Length`  
 任意。 `Integer` 式。 置換する文字数。 省略した場合、`String` のすべてが使われます。  
  
 `StringExpression`  
 必須です。 `Target` の一部を置き換える `String` 式。  
  
## <a name="exceptions"></a>例外  
  
|例外の種類|条件|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|`Start` <= 0 または `Length` < 0。|  
  
## <a name="remarks"></a>Remarks  
 置換される文字数は、常に `Target` の文字数以下です。  
  
 Visual Basic には <xref:Microsoft.VisualBasic.Strings.Mid%2A> 関数と `Mid` ステートメントがあります。 これらの要素は、どちらも文字列内の指定した数の文字に対して操作しますが、`Mid` 関数では文字が返され、`Mid` ステートメントでは文字が置換されます。 詳細については、「<xref:Microsoft.VisualBasic.Strings.Mid%2A>」を参照してください。  
  
> [!NOTE]
> 以前のバージョンの Visual Basic の `MidB` ステートメントでは、文字ではなく、バイト単位で部分文字列が置換されます。 それは主に、2 バイト文字セット (DBCS) アプリケーションで文字列を変換するために使用します。 すべての Visual Basic の文字列は Unicode 形式であり、`MidB` はサポートされなくなりました。  
  
## <a name="example"></a>例  
 この例では、`Mid` ステートメントを使用して、String 変数の指定された数の文字を別の文字列からの文字に置き換えます。  
  
 [!code-vb[VbVbalrStrings#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#5)]  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [Microsoft.VisualBasic](../runtime-library-members.md)  
  
 **モジュール:** `Strings`  
  
 **アセンブリ:** Visual Basic ランタイム ライブラリ (Microsoft.VisualBasic.dll)  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.Mid%2A>
- [文字列](../../programming-guide/language-features/strings/index.md)
- [Visual Basic の文字列の概要](../../programming-guide/language-features/strings/introduction-to-strings.md)
