---
title: アプリケーション フォームへのアクセス
ms.date: 07/20/2015
helpviewer_keywords:
- forms [Visual Basic], communicating between
- application forms [Visual Basic], accessing
- forms [Visual Basic], accessing one from another
- My.Forms object
- forms [Visual Basic], accessing all open
ms.assetid: 9aaf5aaf-2012-4f97-89c7-6e62b9d17863
ms.openlocfilehash: 44f98632fd2fd6c4c087a78b805d5b7da750df87
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410206"
---
# <a name="accessing-application-forms-visual-basic"></a>アプリケーション フォームへのアクセス (Visual Basic)

`My.Forms` オブジェクトは、アプリケーションのプロジェクトで宣言された各 Windows フォームのインスタンスに簡単にアクセスする方法を提供します。 `My.Application` オブジェクトのプロパティを利用し、アプリケーションのスプラッシュ スクリーンとメイン フォームにアクセスし、アプリケーションのオープン フォームの一覧を取得することもできます。  
  
## <a name="tasks"></a>処理手順  

 次の表に示すのは、アプリケーションのフォームにアクセスする方法を示す例です。  
  
|ターゲット|参照先|  
|---|---|  
|アプリケーションのあるフォームから別のフォームにアクセスします。|[My.Forms オブジェクト](../../language-reference/objects/my-forms-object.md)|  
|アプリケーションのすべてのオープン フォームのタイトルを表示します。|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>|  
|アプリケーションの起動時に状態情報でスプラッシュ スクリーンを更新します。|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>|  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>
- [My.Forms オブジェクト](../../language-reference/objects/my-forms-object.md)
