---
title: ユーザー入力の検証
description: Windows フォームを使用して、アプリケーションのユーザー入力を検証するいくつかの方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, validating user input
- validation [Windows Forms], Windows Forms user input
- user input [Windows Forms], validating in Windows Forms
- validating user input [Windows Forms], Windows Forms
ms.assetid: 4ec07681-1dee-4bf9-be5e-718f635a33a1
ms.openlocfilehash: 89f245a523d473f052a337d8f29c2c05105d75eb
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325559"
---
# <a name="user-input-validation-in-windows-forms"></a>Windows フォームでのユーザー入力の検証
ユーザーがアプリケーションにデータを入力するときに、アプリケーションで使用する前にデータが有効であることを確認する必要がある場合があります。 特定のテキストフィールドの長さがゼロでないこと、フィールドが電話番号またはその他の整形式のデータとして書式設定されていること、または、データベースのセキュリティを侵害するために使用できる安全でない文字が文字列に含まれていないことが必要になる場合があります。 Windows フォームには、アプリケーションの入力を検証するためのいくつかの方法が用意されています。  
  
## <a name="validation-with-the-maskedtextbox-control"></a>MaskedTextBox コントロールを使用した検証  
 電話番号や部品番号など、適切に定義された形式でデータを入力するようユーザーに要求する必要がある場合は、コントロールを使用して、この作業をすばやく、最小限のコードで行うことができ <xref:System.Windows.Forms.MaskedTextBox> ます。 *マスク*は、テキストボックス内の任意の位置に入力できる文字を指定するマスク言語の文字から構成される文字列です。 コントロールは、ユーザーにプロンプトのセットを表示します。 ユーザーが正しくないエントリを入力した場合 (たとえば、数字が必要なときにユーザーが文字を入力した場合)、コントロールは自動的に入力を拒否します。  
  
 で使用されるマスク言語 <xref:System.Windows.Forms.MaskedTextBox> は、非常に柔軟です。 必須の文字、オプションの文字、ハイフンとかっこ、通貨記号、日付の区切り記号などのリテラル文字を指定できます。 コントロールは、データソースにバインドされている場合にも適切に機能します。 <xref:System.Windows.Forms.Binding.Format>データバインディングのイベントを使用して、マスクに準拠するように受信データを再フォーマットできます。また、イベントを使用して、 <xref:System.Windows.Forms.Binding.Parse> データフィールドの仕様に準拠するように送信データを再フォーマットできます。  
  
 詳細については、「 [MaskedTextBox Control](./controls/maskedtextbox-control-windows-forms.md)」を参照してください。  
  
## <a name="event-driven-validation"></a>イベントドリブン検証  
 検証を完全に制御する場合、または複雑な検証チェックを実行する必要がある場合は、ほとんどの Windows フォームコントロールに組み込まれている検証イベントを使用する必要があります。 自由形式のユーザー入力を受け入れる各コントロールには、 <xref:System.Windows.Forms.Control.Validating> コントロールがデータの検証を必要とするたびに発生するイベントがあります。 <xref:System.Windows.Forms.Control.Validating>イベント処理メソッドでは、いくつかの方法でユーザー入力を検証できます。 たとえば、郵便番号が含まれている必要のあるテキストボックスがある場合は、次の方法で検証を実行できます。  
  
- 郵便番号が特定の郵便番号グループに属している必要がある場合は、入力に対して文字列比較を実行し、ユーザーが入力したデータを検証することができます。 たとえば、郵便番号が {10001, 10002, 10003} のセットに含まれている必要がある場合は、文字列比較を使用してデータを検証できます。  
  
- 郵便番号が特定の形式である必要がある場合は、正規表現を使用して、ユーザーが入力したデータを検証できます。 たとえば、フォーム `#####` またはを検証するには、 `#####-####` 正規表現を使用し `^(\d{5})(-\d{4})?$` ます。 フォームを検証するには、 `A#A #A#` 正規表現を使用し `[A-Z]\d[A-Z] \d[A-Z]\d` ます。 正規表現の詳細については、「[正規表現](../../standard/base-types/regular-expressions.md)と[正規表現の例](../../standard/base-types/regular-expression-example-scanning-for-hrefs.md)の .NET Framework」を参照してください。  
  
- 郵便番号が有効な米国郵便番号である必要がある場合は、郵便番号 Web サービスを呼び出して、ユーザーが入力したデータを検証することができます。  
  
 <xref:System.Windows.Forms.Control.Validating>イベントには、型のオブジェクトが指定されてい <xref:System.ComponentModel.CancelEventArgs> ます。 コントロールのデータが有効でないと判断した場合は、 <xref:System.Windows.Forms.Control.Validating> このオブジェクトのプロパティをに設定することによって、イベントをキャンセルでき <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> `true` ます。 プロパティを設定しなかった場合 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 、Windows フォームはそのコントロールに対して検証が成功したと想定し、イベントを発生させ <xref:System.Windows.Forms.Control.Validated> ます。  
  
 の電子メールアドレスを検証するコード例につい <xref:System.Windows.Controls.TextBox> ては、「」を参照してください <xref:System.Windows.Forms.Control.Validating> 。  
  
### <a name="data-binding-and-event-driven-validation"></a>データバインディングとイベントドリブン検証  
 検証は、データベーステーブルなどのデータソースにコントロールをバインドした場合に非常に便利です。 検証を使用すると、コントロールのデータがデータソースに必要な形式を満たしていること、および引用符や、安全でない可能性があるバックスラッシュなどの特殊文字が含まれていないことを確認できます。  
  
 データバインディングを使用する場合、コントロール内のデータは、イベントの実行時にデータソースと同期され <xref:System.Windows.Forms.Control.Validating> ます。 イベントをキャンセルした場合、データは <xref:System.Windows.Forms.Control.Validating> データソースと同期されません。  
  
> [!IMPORTANT]
> イベントの後に実行されるカスタム検証がある場合 <xref:System.Windows.Forms.Control.Validating> 、データバインディングには影響しません。 たとえば、データバインディングをキャンセルしようとするイベントにコードがある場合、 <xref:System.Windows.Forms.Control.Validated> データバインディングは引き続き発生します。 この場合、イベントで検証を実行するには、 <xref:System.Windows.Forms.Control.Validated> コントロールの**データソース更新モード**プロパティ (**[(データ連結)** \\ **(詳細)**]) を [ **onvalidation** ] から [**なし**] に変更し、 *Control* `.DataBindings["` *\<YOURFIELD>* `"].WriteValue()` 検証コードにコントロールを追加します。  
  
### <a name="implicit-and-explicit-validation"></a>暗黙的および明示的な検証  
 では、コントロールのデータが検証されるのはいつですか。 これは、開発者が行うことができます。 アプリケーションのニーズに応じて、暗黙的または明示的な検証を使用できます。  
  
#### <a name="implicit-validation"></a>暗黙の検証  
 暗黙的な検証方法では、ユーザーがデータを入力したときにデータが検証されます。 データが押されたときにキーを読み取ることによって、コントロールに入力されたデータを検証することができます。また、ユーザーが入力フォーカスを1つのコントロールから離れて次のコントロールに移動するたびに、より一般的な情報を確認することもできます。 この方法は、作業中のデータに関するフィードバックをユーザーに即時に提供する場合に便利です。  
  
 コントロールに対して暗黙の検証を使用する場合は、そのコントロールの <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> プロパティをまたはに設定する必要があり <xref:System.Windows.Forms.AutoValidate.EnablePreventFocusChange> <xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange> ます。 イベントを取り消すと <xref:System.Windows.Forms.Control.Validating> 、コントロールの動作は、割り当てた値によって決まり <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> ます。 割り当てた場合 <xref:System.Windows.Forms.AutoValidate.EnablePreventFocusChange> 、イベントのキャンセルによって <xref:System.Windows.Forms.Control.Validated> イベントが発生しません。 入力フォーカスは、ユーザーがデータを有効な入力に変更するまで、現在のコントロールにとどまります。 を割り当てた場合、イベントをキャンセルして <xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange> <xref:System.Windows.Forms.Control.Validated> もイベントは発生しませんが、フォーカスは次のコントロールに変わります。  
  
 <xref:System.Windows.Forms.AutoValidate.Disable>プロパティにを割り当てると、 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 暗黙的な検証がまったく行われません。 コントロールを検証するには、明示的な検証を使用する必要があります。  
  
#### <a name="explicit-validation"></a>明示的な検証  
 明示的な検証方法では、データを一度に検証します。 [保存] ボタンまたは次のリンクをクリックするなど、ユーザーの操作に応じてデータを検証できます。 ユーザーアクションが発生すると、次のいずれかの方法で明示的な検証をトリガーできます。  
  
- を呼び出して <xref:System.Windows.Forms.ContainerControl.Validate%2A> 、最後のコントロールがフォーカスを失ったことを検証します。  
  
- を呼び出して <xref:System.Windows.Forms.ContainerControl.ValidateChildren%2A> 、フォームまたはコンテナーコントロール内のすべての子コントロールを検証します。  
  
- カスタムメソッドを呼び出して、コントロール内のデータを手動で検証します。  
  
#### <a name="default-implicit-validation-behavior-for-windows-forms-controls"></a>Windows フォームコントロールの既定の暗黙的な検証動作  
 さまざまな Windows フォームコントロールのプロパティの既定値は異なり <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> ます。 次の表は、最も一般的なコントロールとその既定値を示しています。  
  
|コントロール|既定の検証動作|  
|-------------|---------------------------------|  
|<xref:System.Windows.Forms.ContainerControl>|<xref:System.Windows.Forms.AutoValidate.Inherit>|  
|<xref:System.Windows.Forms.Form>|<xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange>|  
|<xref:System.Windows.Forms.PropertyGrid>|プロパティが Visual Studio で公開されていません|  
|<xref:System.Windows.Forms.ToolStripContainer>|プロパティが Visual Studio で公開されていません|  
|<xref:System.Windows.Forms.SplitContainer>|<xref:System.Windows.Forms.AutoValidate.Inherit>|  
|<xref:System.Windows.Forms.UserControl>|<xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange>|  
  
## <a name="closing-the-form-and-overriding-validation"></a>フォームを閉じ、検証をオーバーライドする  
 コントロールが、格納されているデータが無効なためにフォーカスを保持する場合、通常の方法のいずれかで親フォームを閉じることはできません。  
  
- [**閉じる**] ボタンをクリックします。  
  
- [**システム**] メニューの [**閉じる**] を選択します。  
  
- プログラムによってメソッドを呼び出し <xref:System.Windows.Forms.Form.Close%2A> ます。  
  
 ただし、場合によっては、コントロールの値が有効かどうかに関係なく、ユーザーがフォームを閉じることが必要になることがあります。 フォームのイベントのハンドラーを作成することにより、検証をオーバーライドして、無効なデータがまだ含まれているフォームを閉じることができ <xref:System.Windows.Forms.Form.FormClosing> ます。 イベントで、 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> プロパティをに設定し `false` ます。 これにより、フォームが強制的に閉じられます。 使用例を含む詳細については、「<xref:System.Windows.Forms.Form.FormClosing?displayProperty=nameWithType>」を参照してください。  
  
> [!NOTE]
> フォームがこのように強制的に閉じられるようにすると、フォームのコントロールに保存されていないデータはすべて失われます。 また、モーダルフォームは、コントロールが閉じられたときに、その内容を検証しません。 コントロールの検証を引き続き使用してコントロールにフォーカスを移すことはできますが、フォームの終了に関連する動作について心配する必要はありません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Control.Validating?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Form.FormClosing?displayProperty=nameWithType>
- <xref:System.Windows.Forms.FormClosingEventArgs?displayProperty=nameWithType>
- [MaskedTextBox コントロール](./controls/maskedtextbox-control-windows-forms.md)
- [正規表現の例](../../standard/base-types/regular-expression-example-scanning-for-hrefs.md)
