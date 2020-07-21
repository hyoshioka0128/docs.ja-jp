---
title: コントロールのタブオーダーを設定する
description: Windows フォームのコントロールのタブオーダーを設定する方法について説明します。 タブオーダーを Visual Studio で設定するか、プロパティウィンドウの TabIndex プロパティを使用します。
ms.date: 03/30/2017
f1_keywords:
- TabStop
- TabIndex
helpviewer_keywords:
- tab order [Windows Forms], controls on Windows forms
- Windows Forms controls, setting tab order
- controls [Windows Forms], setting tab order
- Windows Forms, setting tab order
ms.assetid: 71fa8e76-0472-414b-ad3c-0f90166e0ad7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3d16da1ac73cc030b92bb36c4bfa3a79985339bf
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903363"
---
# <a name="how-to-set-the-tab-order-on-windows-forms"></a>方法: Windows フォームのタブオーダーを設定する

タブオーダーは、Tab キーを押すことによって、ユーザーがあるコントロールから別のコントロールにフォーカスを移動する順序です。 各フォームには、独自のタブオーダーがあります。 既定では、タブオーダーは、コントロールを作成した順序と同じです。 タブオーダー番号は0から始まります。

## <a name="to-set-the-tab-order-of-a-control"></a>コントロールのタブオーダーを設定するには

1. Visual Studio の [**表示**] メニューで、[**タブオーダー**] を選択します。

   これにより、フォームのタブオーダー選択モードがアクティブになります。 <xref:System.Windows.Forms.Control.TabIndex%2A>各コントロールの左上隅に、(プロパティを表す) 数値が表示されます。

2. コントロールを順番にクリックして、目的のタブオーダーを設定します。

   > [!NOTE]
   > タブオーダー内のコントロールの位置は、0以上の任意の値に設定できます。 重複が発生すると、2つのコントロールの z オーダーが評価され、上のコントロールが最初にタブになります。 (Z オーダーは、フォームの z 軸の [奥行] に沿ったフォーム上のコントロールの視覚的なレイヤーです。 Z オーダーは、他のコントロールの前にあるコントロールを決定します。)Z オーダーの詳細については、「 [Windows フォームのオブジェクトのレイヤー](how-to-layer-objects-on-windows-forms.md)化」を参照してください。

3. 終了したら、[**表示**] メニューの [**タブオーダー** ] をもう一度選択して、タブオーダーモードを終了します。

   > [!NOTE]
   > フォーカスを取得できず、無効になったコントロールや非表示のコントロールでも、プロパティはなく、 <xref:System.Windows.Forms.Control.TabIndex%2A> タブオーダーには含まれません。 ユーザーが Tab キーを押すと、これらのコントロールはスキップされます。

また、プロパティを使用して、プロパティウィンドウでタブオーダーを設定することもでき <xref:System.Windows.Forms.Control.TabIndex%2A> ます。 <xref:System.Windows.Forms.Control.TabIndex%2A>コントロールのプロパティは、タブオーダー内での位置を決定します。 既定では、描画された最初のコントロールの <xref:System.Windows.Forms.Control.TabIndex%2A> 値は0、2番目のコントロールのは <xref:System.Windows.Forms.Control.TabIndex%2A> 1、などです。

また、既定では、コントロールには、整数である <xref:System.Windows.Forms.GroupBox> 独自の値があり <xref:System.Windows.Forms.Control.TabIndex%2A> ます。 コントロール自体には、 <xref:System.Windows.Forms.GroupBox> 実行時にフォーカスを設定することはできません。 したがって、内の各コントロール <xref:System.Windows.Forms.GroupBox> には、 <xref:System.Windows.Forms.Control.TabIndex%2A> 0 から始まる独自の10進値があります。 当然ながら、コントロールのがインクリメントされると、 <xref:System.Windows.Forms.Control.TabIndex%2A> <xref:System.Windows.Forms.GroupBox> その中のコントロールがそれに応じてインクリメントされます。 <xref:System.Windows.Forms.Control.TabIndex%2A>値を5から6に変更した場合、 <xref:System.Windows.Forms.Control.TabIndex%2A> そのグループの最初のコントロールの値は自動的に6.0 に変更されます。

最後に、フォーム上の多くのコントロールは、タブオーダーではスキップできます。 通常、実行時に Tab キーを連続して押すと、各コントロールがタブオーダーで選択されます。 プロパティをオフに <xref:System.Windows.Forms.Control.TabStop%2A> すると、フォームのタブオーダーでコントロールを渡すことができます。

## <a name="to-remove-a-control-from-the-tab-order"></a>タブオーダーからコントロールを削除するには

<xref:System.Windows.Forms.Control.TabStop%2A>[**プロパティ**] ウィンドウで、コントロールのプロパティを**false**に設定します。

<xref:System.Windows.Forms.Control.TabStop%2A>Tab キーを使用してコントロールを `false` 巡回するときにコントロールがスキップされる場合でも、プロパティがに設定されているコントロールは、タブオーダーの位置を維持します。

> [!NOTE]
> ラジオボタングループには、実行時に1つのタブストップがあります。 選択したボタン (プロパティがに設定されているボタン) では、プロパティが自動的にに設定され、 <xref:System.Windows.Forms.RadioButton.Checked%2A> `true` <xref:System.Windows.Forms.Control.TabStop%2A> `true` 他のボタンの <xref:System.Windows.Forms.Control.TabStop%2A> プロパティはに設定され `false` ます。 コントロールのグループ化の詳細については <xref:System.Windows.Forms.RadioButton> 、「 [Set Windows フォーム RadioButton コントロールをセットとして機能させる](how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [Windows フォームコントロール](index.md)
- [Windows フォームで使用するコントロール](controls-to-use-on-windows-forms.md)
- [Windows フォーム コントロールの機能別一覧](windows-forms-controls-by-function.md)
