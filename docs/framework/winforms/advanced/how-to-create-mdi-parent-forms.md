---
title: '方法: MDI 親フォームを作成する'
description: プログラムによって、または Windows フォームデザイナーを使用して、MDI 親フォームを作成する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- parent forms
- MDI [Windows Forms], creating forms
ms.assetid: 12c71221-2377-4bb6-b10b-7b4b300fd462
ms.openlocfilehash: d387837a565ca247f62828c19f353990b35117c7
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174706"
---
# <a name="how-to-create-mdi-parent-forms"></a>方法: MDI 親フォームを作成する

> [!IMPORTANT]
> このトピックでは、既に <xref:System.Windows.Forms.MainMenu> コントロールで置き換えられている <xref:System.Windows.Forms.MenuStrip> コントロールを使用します。 <xref:System.Windows.Forms.MainMenu> コントロールは、下位互換性と将来の使用 (必要に応じて) の両方のために保持されています。 を使用した MDI 親フォームの作成の詳細については <xref:System.Windows.Forms.MenuStrip> 、「[方法: MenuStrip を](../controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)使用して Mdi ウィンドウの一覧を作成する」を参照してください。

マルチドキュメント インターフェイス (MDI) アプリケーションの基盤となるのは、MDI 親フォームです。 これは、サブウィンドウである MDI 子ウィンドウを含むフォームで、ユーザーは MDI 子ウィンドウで MDI アプリケーションと対話します。 MDI 親フォームの作成は簡単で、Windows フォーム デザイナーまたはプログラムで作成できます。

## <a name="create-an-mdi-parent-form-at-design-time"></a>デザイン時に MDI 親フォームを作成する

1. Visual Studio で Windows アプリケーションプロジェクトを作成します。

2. [**プロパティ**] ウィンドウで、 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> プロパティを**true**に設定します。

     これによって、フォームが子ウィンドウの MDI コンテナーとして指定されます。

    > [!NOTE]
    > **[プロパティ]** ウィンドウでプロパティを設定するときに、必要に応じて、`WindowState` プロパティを **[Maximized]** に設定することもできます。MDI 子ウィンドウは、親フォームが最大化しているときに最も簡単に操作できます。 また、MDI 親フォームの端には、<xref:System.Windows.Forms.Control.BackColor%2A?displayProperty=nameWithType> プロパティを使用して設定した背景色ではなく、(Windows システムのコントロール パネルで設定した) システム カラーが適用されることに注意してください。

3. **[ツールボックス]** から、**[MenuStrip]** コントロールをフォームにドラッグします。 **Text** プロパティを「**ファイル (F)**」に設定し、「**新規作成 (N)**」と「**閉じる (C)**」というサブメニュー項目を指定して、トップレベルのメニュー項目を作成します。 また、「**ウィンドウ (W)**」というトップレベルのメニュー項目も作成します。

     最初のメニューでは、実行時にメニュー項目を作成したり非表示にしたりします。2 つ目のメニューでは、開いている MDI 子ウィンドウを追跡します。 これで、MDI 親ウィンドウの作成が完了しました。

4. **F5** キーを押してアプリケーションを実行します。 MDI 親フォーム内で動作する MDI 子ウィンドウの作成方法の詳細については、「[方法: MDI 子フォームを作成する](how-to-create-mdi-child-forms.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [マルチ ドキュメント インターフェイス (MDI) アプリケーション](multiple-document-interface-mdi-applications.md)
- [方法: MDI 子フォームを作成する](how-to-create-mdi-child-forms.md)
- [方法: アクティブな MDI 子フォームを特定する](how-to-determine-the-active-mdi-child.md)
- [方法: アクティブな MDI 子フォームにデータを送信する](how-to-send-data-to-the-active-mdi-child.md)
- [方法: MDI 子フォームを配置する](how-to-arrange-mdi-child-forms.md)
