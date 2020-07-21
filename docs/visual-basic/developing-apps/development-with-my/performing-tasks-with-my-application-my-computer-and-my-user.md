---
title: My.Application、My.Computer、および My.User でのタスクの実行
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application object [Visual Basic], developing applications
- rapid application development (RAD), My.Application
- rapid application development (RAD), My.Computer
- rapid application development (RAD), My.User
- My.Computer object [Visual Basic], developing applications
- My.User object [Visual Basic], developing applications
ms.assetid: c8af61bd-4dd3-4a0f-9af5-795b594b240b
ms.openlocfilehash: 55961d6857b690fc2726f541df8a5497a3207928
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411695"
---
# <a name="performing-tasks-with-myapplication-mycomputer-and-myuser-visual-basic"></a>My.Application、My.Computer、および My.User でのタスクの実行 (Visual Basic)

情報へのアクセスとよく使用される機能が提供される中心的な 3 つの `My` オブジェクトが、`My.Application` (<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>)、`My.Computer` (<xref:Microsoft.VisualBasic.Devices.Computer>)、`My.User` (<xref:Microsoft.VisualBasic.ApplicationServices.User>) です。 これらのオブジェクトを使用してそれぞれ、現在のアプリケーション、アプリケーションがインストールされているコンピューター、またはアプリケーションの現在のユーザーに関連する情報にアクセスできます。  
  
## <a name="myapplication-mycomputer-and-myuser"></a>My.Application、My.Computer、My.User  

 次の例は、`My` を使用して情報を取得する方法を示しています。  
  
 [!code-vb[VbVbcnMy#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#1)]  
  
 [!code-vb[VbVbcnMy#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#2)]  
  
 情報を取得するだけでなく、これら 3 つのオブジェクトを使用して公開されるメンバーは、そのオブジェクトに関連するメソッドを実行することもできます。 たとえば、`My.Computer` を使用して、さまざまなメソッドにアクセスして、ファイルの操作やレジストリの更新ができます。  
  
 ファイル、ディレクトリ、およびドライブを操作するためのさまざまなメソッドとプロパティが含まれているため、`My` を使用するとファイル I/O が大幅に簡単で高速になります。 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> オブジェクトを使用すると、区切り記号または固定幅フィールドが含まれる大規模な構造化ファイルから読み取ることができます。 この例では、`TextFieldParser` `reader` を開き、それを使用して `C:\TestFolder1\test1.txt` から読み取ります。  
  
 [!code-vb[VbVbalrTextFieldParser#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTextFieldParser/VB/Class1.vb#23)]  
  
 `My.Application` アプリケーションを使用すると、アプリケーションのカルチャを変更できます。 このメソッドを呼び出す方法を次の例に示します。  
  
 [!code-vb[VbVbcnMy#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [プロジェクトの種類に応じた My の機能](how-my-depends-on-project-type.md)
