---
title: スタートアップ フォームが指定されていません。
ms.date: 07/20/2015
f1_keywords:
- vbrAppModel_NoStartupForm
ms.assetid: 8e04af49-4bef-49de-a7ec-e407e9873da7
ms.openlocfilehash: 058deb1378ed9218274ae20c8340178f7c8fa58c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409908"
---
# <a name="a-startup-form-has-not-been-specified"></a>スタートアップ フォームが指定されていません。

アプリケーションで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> クラスが使用されていますが、スタートアップ フォームが指定されていません。  
  
 これは、プロジェクト デザイナーで **[アプリケーション フレームワークを有効にする]** チェック ボックスがオンになっていても、 **[スタートアップ フォーム]** が指定されていない場合に発生する可能性があります。 詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)」を参照してください。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. アプリケーションのスタートアップ オブジェクトを指定します。  
  
     詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)」を参照してください。  
  
2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> メソッドをオーバーライドして、スタートアップ フォームに <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> プロパティを設定します。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A>
- [Visual Basic アプリケーション モデルの概要](../../developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)
