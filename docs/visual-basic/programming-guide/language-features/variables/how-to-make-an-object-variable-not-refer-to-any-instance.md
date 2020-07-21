---
title: '方法: オブジェクト変数がインスタンスを参照しないようにする'
ms.date: 07/20/2015
helpviewer_keywords:
- Nothing keyword [Visual Basic], variable assignment
- object variables [Visual Basic], null reference
ms.assetid: e6d30578-bdae-4142-a3ac-a10697bf696a
ms.openlocfilehash: cce2e59cb76652937868a731ad308872d1aba2f3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410452"
---
# <a name="how-to-make-an-object-variable-not-refer-to-any-instance-visual-basic"></a>方法: オブジェクト変数がインスタンスを参照しないようにする (Visual Basic)
オブジェクト変数を [Nothing](../../../language-reference/nothing.md) に設定すると、任意のオブジェクト インスタンスとの関連付けを解除できます。  
  
### <a name="to-disassociate-an-object-variable-from-any-object-instance"></a>オブジェクト変数とオブジェクト インスタンスの関連付けを解除するには  
  
- 代入ステートメントで変数を `Nothing` に設定します。  
  
    ```vb  
    ' Assume account is a defined class  
    Dim currentAccount As account  
    currentAccount = Nothing  
    ```  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 コードで、`Nothing` に設定されているオブジェクト変数のメンバーにアクセスしようとすると、<xref:System.NullReferenceException> が発生します。 オブジェクト変数を頻繁に `Nothing` に設定する場合、または変数が初期化されていない可能性がある場合は、メンバー アクセスを `Try...Catch...Finally` ブロックで囲むことをお勧めします。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 機密データを含むオブジェクトに対してオブジェクト変数を使用する場合は、これらのオブジェクトのいずれかをアクティブに処理していないときに、この変数を `Nothing` に設定できます。 これにより、悪意のあるコードからデータにアクセスされる可能性が低くなります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.NullReferenceException>
- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の代入](object-variable-assignment.md)
- [Nothing](../../../language-reference/nothing.md)
- [Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)
