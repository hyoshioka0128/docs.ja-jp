---
title: マルチ ドキュメント インターフェイス (MDI) アプリケーション
description: マルチドキュメントインターフェイス (MDI) アプリケーションを使用して複数のドキュメントを同時に表示する Windows フォーム方法について説明します。各ドキュメントは、それぞれのウィンドウに表示されます。
ms.date: 03/30/2017
helpviewer_keywords:
- forms [Windows Forms], MDI
- windows [Windows Forms], mDI
- Windows Forms, MDI applications
- MDI
ms.assetid: 599faf75-13cf-49cc-ad3c-255545e5cb97
ms.openlocfilehash: 0912a989ac1710d72c9db1cceb0e695f0ca85dee
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174654"
---
# <a name="multiple-document-interface-mdi-applications"></a>マルチ ドキュメント インターフェイス (MDI) アプリケーション
マルチドキュメントインターフェイス (MDI) アプリケーションを使用すると、複数のドキュメントを同時に表示することができ、各ドキュメントは独自のウィンドウに表示されます。 MDI アプリケーションには、多くの場合、ウィンドウまたはドキュメントを切り替えるためのサブメニューを含む [ウィンドウ] メニュー項目があります。  
  
> [!NOTE]
> Windows フォームの MDI フォームとシングルドキュメントインターフェイス (SDI) ウィンドウには、いくつかの動作の違いがあります。 プロパティは、 `Opacity` MDI 子フォームの外観には影響しません。 また、メソッドは、 <xref:System.Windows.Forms.Form.CenterToParent%2A> MDI 子フォームの動作には影響しません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: MDI 親フォームを作成する](how-to-create-mdi-parent-forms.md)  
 MDI アプリケーション内の複数のドキュメントのコンテナーを作成する方法について説明します。  
  
 [方法: MDI 子フォームを作成する](how-to-create-mdi-child-forms.md)  
 MDI 親フォーム内で動作する1つまたは複数のウィンドウを作成する方法を示します。  
  
 [方法: アクティブな MDI 子フォームを特定する](how-to-determine-the-active-mdi-child.md)  
 フォーカスのある子ウィンドウを確認し、その内容をクリップボードに送信する方法を示します。  
  
 [方法: アクティブな MDI 子フォームにデータを送信する](how-to-send-data-to-the-active-mdi-child.md)  
 アクティブな子ウィンドウに情報を転送する方法を示します。  
  
 [方法: MDI 子フォームを配置する](how-to-arrange-mdi-child-forms.md)  
 MDI アプリケーションの子ウィンドウを並べて配置したり、整列したりするための手順を示します。
