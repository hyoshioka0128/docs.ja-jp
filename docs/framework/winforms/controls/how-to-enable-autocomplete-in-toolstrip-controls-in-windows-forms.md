---
title: '方法 : ToolStrip コントロールの AutoComplete を有効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutoComplete [Windows Forms], examples
- toolbars [Windows Forms], AutoComplete
- examples [Windows Forms], toolbars
- AutoComplete [Windows Forms], enabling in toolbars
- ToolStripComboBox class [Windows Forms], examples
- ToolStrip control [Windows Forms], AutoComplete
ms.assetid: fd66d085-1af1-45d4-930a-cde944da2e16
ms.openlocfilehash: 18b17aaea9d2354c03bb43f3fdd8d3779697cf58
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142019"
---
# <a name="how-to-enable-autocomplete-in-toolstrip-controls-in-windows-forms"></a>方法 : Windows フォームで ToolStrip コントロールの AutoComplete を有効にする
次の手順では、<xref:System.Windows.Forms.ToolStripLabel>とを<xref:System.Windows.Forms.ToolStripComboBox>組み合わせて、ドロップ ダウンして、最近アクセスした Web サイトなどのアイテムの一覧を表示します。 ユーザーがリスト内の項目の 1 つの最初の文字と一致する文字を入力すると、その項目は直ちに表示されます。  
  
> [!NOTE]
> オートコンプリート`ToolStrip`は、 や などの<xref:System.Windows.Forms.ComboBox>従来のコントロールと同じようにコントロールを<xref:System.Windows.Forms.TextBox>操作します。  
  
### <a name="to-enable-autocomplete-in-a-toolstrip-control"></a>ツールストリップ コントロールでオートコンプリートを有効にするには  
  
1. コントロールを<xref:System.Windows.Forms.ToolStrip>作成し、それに項目を追加します。  
  
    ```vb  
    ToolStrip1 = New System.Windows.Forms.ToolStrip  
    ToolStrip1.Items.AddRange(New System.Windows.Forms.ToolStripItem()_  
        {ToolStripLabel1, ToolStripComboBox1})  
    ```  
  
    ```csharp  
    toolStrip1 = new System.Windows.Forms.ToolStrip();  
    toolStrip1.Items.AddRange(new System.Windows.Forms.ToolStripItem[]
        {toolStripLabel1, toolStripComboBox1});  
    ```  
  
2. フォームの<xref:System.Windows.Forms.ToolStripItem.Overflow%2A>サイズに関係なくリストを常に<xref:System.Windows.Forms.ToolStripItemOverflow.Never>使用できるように、ラベルとコンボ ボックスのプロパティを設定します。  
  
    ```vb  
    ToolStripLabel1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    ToolStripComboBox1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    ```  
  
    ```csharp  
    toolStripLabel1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    toolStripComboBox1.Overflow = System.Windows.Forms.ToolStripItemOverflow.Never  
    ```  
  
3. コントロールの Items コレクションに単語<xref:System.Windows.Forms.ToolStripComboBox>を追加します。  
  
    ```vb  
    ToolStripComboBox1.Items.AddRange(New Object() {"First Item", _  
        "Second Item", "Third Item"})  
    ```  
  
    ```csharp  
    toolStripComboBox1.Items.AddRange(new object[] {"First item", "Second item", "Third item"});  
    ```  
  
4. コンボ<xref:System.Windows.Forms.ComboBox.AutoCompleteMode%2A>ボックスのプロパティを に<xref:System.Windows.Forms.AutoCompleteMode.Append>設定します。  
  
    ```vb  
    ToolStripComboBox1.AutoCompleteMode = _  
        System.Windows.Forms.AutoCompleteMode.Append  
    ```  
  
    ```csharp  
    toolStripComboBox1.AutoCompleteMode = System.Windows.Forms.AutoCompleteMode.Append;  
    ```  
  
5. コンボ<xref:System.Windows.Forms.ComboBox.AutoCompleteSource%2A>ボックスのプロパティを に<xref:System.Windows.Forms.AutoCompleteSource.ListItems>設定します。  
  
    ```vb  
    ToolStripComboBox1.AutoCompleteSource = _  
        System.Windows.Forms.AutoCompleteSource.ListItems  
    ```  
  
    ```csharp  
    toolStripComboBox1.AutoCompleteSource = System.Windows.Forms.AutoCompleteSource.ListItems;  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripLabel>
- <xref:System.Windows.Forms.ToolStripComboBox>
- <xref:System.Windows.Forms.ToolStripComboBox.AutoCompleteMode%2A>
- <xref:System.Windows.Forms.ToolStripComboBox.AutoCompleteSource%2A>
- [ToolStrip コントロールの概要](toolstrip-control-overview-windows-forms.md)
- [ToolStrip コントロールのアーキテクチャ](toolstrip-control-architecture.md)
- [ToolStrip テクノロジの概要](toolstrip-technology-summary.md)
