---
title: My.Resources と My.Settings による Rapid Application Development
ms.date: 07/20/2015
helpviewer_keywords:
- My.Settings object [Visual Basic], developing applications
- rapid application development (RAD), My.Resources
- rapid application development (RAD), My.Settings
- My.Resources object [Visual Basic], developing applications
ms.assetid: 68284ab1-b685-4814-a2a4-01ae40445ff8
ms.openlocfilehash: fd1ec25582e919b84235502f5921edfbc6e1dade
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990211"
---
# <a name="rapid-application-development-with-myresources-and-mysettings-visual-basic"></a>My.Resources と My.Settings による Rapid Application Development (Visual Basic)

`My.Resources` オブジェクトは、アプリケーションのリソースへのアクセスを提供し、アプリケーションのリソースを動的に取得できるようにします。  
  
## <a name="retrieving-resources"></a>リソースの取得  

 `My.Resources` オブジェクトを使用して、オーディオ ファイル、アイコン、イメージ、文字列などのさまざまなリソースを取得できます。 例えば、アプリケーションのカルチャ固有のリソース ファイルにアクセスできます。 次の例では、フォームのアイコンを、アプリケーションのリソース ファイルに格納されている `Form1Icon` という名前のアイコンに設定します。  
  
 [!code-vb[VbVbcnMy#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#7)]  
  
 `My.Resources` オブジェクトは、グローバル リソースのみを公開します。 フォームに関連付けられたリソース ファイルへのアクセスは提供しません。 フォームのリソースには、フォームからアクセスします。  
  
 同様に、`My.Settings` オブジェクトは、アプリケーションの設定へのアクセスを提供し、アプリケーションのプロパティ設定やその他の情報を動的に格納し、取得できるようにします。 詳細については、「[My.Resources オブジェクト](../../language-reference/objects/my-resources-object.md)」と「[My.Settings オブジェクト](../../language-reference/objects/my-settings-object.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [My.Resources オブジェクト](../../language-reference/objects/my-resources-object.md)
- [My.Settings オブジェクト](../../language-reference/objects/my-settings-object.md)
- [アプリケーション設定へのアクセス](../programming/app-settings/index.md)
