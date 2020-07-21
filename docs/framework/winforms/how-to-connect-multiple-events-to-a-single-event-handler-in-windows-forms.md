---
title: '方法: 複数のイベントを1つのイベントハンドラーに接続する'
description: C# のプロパティウィンドウのイベントビューを使用して Windows フォームの1つのイベントハンドラーに複数のイベントを接続する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- events [Windows Forms], connecting multiple to single event handler
- event handlers [Windows Forms], connecting events to
- menus [Windows Forms], event-handling methods for multiple menu items
- Windows Forms controls, events
- menu items [Windows Forms], multicasting event-handling methods
ms.assetid: 5a20749a-41b5-4acc-8eb1-9e5040b0a2c4
ms.openlocfilehash: cca85c223b46d9a82dbc3e34e3377fb83c075959
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621887"
---
# <a name="how-to-connect-multiple-events-to-a-single-event-handler-in-windows-forms"></a>方法: Windows フォームの 1 つのイベント ハンドラーに複数のイベントを関連付ける
アプリケーションの設計では、複数のイベントに対して単一のイベントハンドラーを使用するか、複数のイベントで同じ手順を実行する必要があります。 たとえば、多くの場合、メニューコマンドで同じ機能を公開すると、フォーム上のボタンと同じイベントが生成されます。 これを行うには、C# のプロパティウィンドウのイベントビューを使用するか、 `Handles` Visual Basic コードエディターで、キーワードと**クラス名**と**メソッド名**のドロップダウンボックスを使用します。  
  
### <a name="to-connect-multiple-events-to-a-single-event-handler-in-visual-basic"></a>複数のイベントを Visual Basic の1つのイベントハンドラーに接続するには  
  
1. フォームを右クリックし、[**コードの表示**] を選択します。  
  
2. [**クラス名**] ボックスの一覧で、イベントハンドラーが処理するコントロールの1つを選択します。  
  
3. [**メソッド名**] ボックスの一覧で、イベントハンドラーが処理するイベントの1つを選択します。  
  
4. コードエディターによって、適切なイベントハンドラーが挿入され、メソッド内に挿入ポイントが配置されます。 次の例では、 <xref:System.Windows.Forms.Control.Click> コントロールのイベントです <xref:System.Windows.Forms.Button> 。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
5. 処理するその他のイベントを句に追加し `Handles` ます。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click, Button2.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
6. 適切なコードをイベントハンドラーに追加します。  
  
### <a name="to-connect-multiple-events-to-a-single-event-handler-in-c"></a>C で複数のイベントを1つのイベントハンドラーに接続するには\#
  
1. イベントハンドラーを接続するコントロールを選択します。  
  
2. プロパティウィンドウで、[**イベント**] ボタン ([![イベント] ボタン](./media/vxeventsbutton-propertieswindow.png "vxEventsButton_PropertiesWindow")) をクリックします。  
  
3. 処理するイベントの名前をクリックします。  
  
4. イベント名の横にある [値] セクションで、ドロップダウンボタンをクリックして、処理するイベントのメソッドシグネチャに一致する既存のイベントハンドラーの一覧を表示します。  
  
5. 一覧から適切なイベントハンドラーを選択します。  
  
     イベントを既存のイベントハンドラーにバインドするためのコードがフォームに追加されます。  
  
## <a name="see-also"></a>関連項目

- [Windows フォーム内でのイベント ハンドラーの作成](creating-event-handlers-in-windows-forms.md)
- [イベント ハンドラーの概要](event-handlers-overview-windows-forms.md)
