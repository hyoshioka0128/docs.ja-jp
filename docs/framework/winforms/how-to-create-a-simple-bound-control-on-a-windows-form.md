---
title: '方法: Windows フォームに単純バインド コントロールを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [Windows Forms], simple data binding
- Windows Forms controls, data binding
ms.assetid: 3bcaded8-0f1a-4cc0-8830-f59be253bf4e
ms.openlocfilehash: df87f00e6e03de67c3fb1adc28472c96f4a47ef4
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015633"
---
# <a name="how-to-create-a-simple-bound-control-on-a-windows-form"></a>方法: Windows フォームに単純バインドコントロールを作成する

*単純なバインド*では、データセットテーブルの列値など、1つのデータ要素をコントロールに表示できます。 コントロールの任意のプロパティをデータ値に単純にバインドできます。

## <a name="to-simple-bind-a-control"></a>コントロールを単純にバインドするには

1. データ ソースに接続します。 詳細については、「[データソースへの接続](../data/adonet/connecting-to-a-data-source.md)」を参照してください。

2. Visual Studio でフォーム上のコントロールを選択し、 **[プロパティ]** ウィンドウを表示します。

3. **[(連結)]** プロパティを展開します。

     最も頻繁にバインドされるプロパティは、 **([連結])** プロパティの下に表示されます。 たとえば、ほとんどのコントロールでは、 **Text**プロパティは最も頻繁にバインドされます。

4. バインドするプロパティが一般的にバインドされるプロパティの1つでない場合は、 **[(詳細)]** ボックスの**省略記号**ボタン![(省略記号ボタン ..](./media/how-to-create-a-simple-bound-control-on-a-windows-form/visual-studio-ellipsis-button.png)プロパティウィンドウ.) をクリックして、 **[書式設定と詳細バインド**] ダイアログボックスで、そのコントロールのプロパティの完全な一覧が表示されます。

5. バインドするプロパティを選択し、 **[バインド]** の下にあるドロップダウン矢印をクリックします。

     使用できるデータ ソースの一覧が表示されます。

6. 目的の 1 つのデータ要素が見つかるまで、バインド先のデータ ソースを展開します。 たとえば、データセットのテーブル内の列の値にバインドする場合は、データセットの名前を展開し、次にテーブル名を展開して、列名を表示します。

7. バインド先の要素の名前をクリックします。

8. **[書式設定と詳細バインド]** ダイアログボックスで作業している場合は、 **[OK]** をクリックして、 **[プロパティ]** ウィンドウに戻ります。

9. コントロールの追加のプロパティをバインドする場合は、手順 3. ~ 7. を繰り返します。

    > [!NOTE]
    > 単純バインドコントロールにはデータ要素が1つだけ表示されるため、単純バインドコントロールを含む Windows フォームにナビゲーションロジックを含めるのが一般的です。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Binding>
- [Windows フォームでのデータ バインディング](windows-forms-data-binding.md)
- [データ連結と Windows フォーム](data-binding-and-windows-forms.md)
