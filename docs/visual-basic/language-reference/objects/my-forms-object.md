---
title: My.Forms オブジェクト
ms.date: 07/20/2015
f1_keywords:
- My.Forms
- My.MyProject.Forms
helpviewer_keywords:
- My.Forms object
ms.assetid: f6bff4e6-6769-4294-956b-037aa6106d2a
ms.openlocfilehash: 001f6fbfae2467ea0af5e98ca041b694d1e7b8f9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372441"
---
# <a name="myforms-object"></a>My.Forms オブジェクト

現在のプロジェクトで宣言されている各 Windows フォームのインスタンスにアクセスするためのプロパティを提供します。

## <a name="remarks"></a>Remarks

`My.Forms` オブジェクトは、現在のプロジェクトで各フォームのインスタンスを提供します。 プロパティの名前は、プロパティがアクセスするフォームの名前と同じになります。

`My.Forms` オブジェクトによって提供されるフォームにアクセスするには、修飾子を付けずにフォームの名前を使用します。 プロパティ名はフォームの型名と同じであるため、これによって既定のインスタンスがあるかのようにフォームにアクセスできます。 たとえば、`My.Forms.Form1.Show` は、`Form1.Show` と同じです。

`My.Forms` オブジェクトでは、現在のプロジェクトに関連付けられているフォームのみが公開されます。 参照されている DLL で宣言されているフォームへのアクセスは提供されません。 DLL によって提供されるフォームにアクセスするには、 *DllName*.*FormName* として記述されたフォームの修飾名を使用する必要があります。

<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A> プロパティを使用して、すべてのアプリケーションの開いているフォームのコレクションを取得できます。

オブジェクトとそのプロパティは、Windows アプリケーションでのみ使用できます。

## <a name="properties"></a>プロパティ

`My.Forms` オブジェクトの各プロパティにより、現在のプロジェクトのフォームのインスタンスにアクセスできます。 プロパティの名前は、プロパティがアクセスするフォームの名前と同じになり、プロパティの型はフォームの型と同じになります。

> [!NOTE]
> 名前の競合がある場合、フォームにアクセスするためのプロパティ名は、*RootNamespace*_*Namespace*\_*FormName* になります。 たとえば、`Form1.` という名前の 2 つのフォームを考えてみます。これらのフォームのいずれかがルート名前空間 `WindowsApplication1` と名前空間 `Namespace1` にある場合、`My.Forms.WindowsApplication1_Namespace1_Form1` によってそのフォームにアクセスします。

`My.Forms` オブジェクトでは、起動時に作成されたアプリケーションのメイン フォームのインスタンスにアクセスできます。 その他のすべてのフォームの場合、`My.Forms` オブジェクトによって、アクセス時にフォームの新しいインスタンスが作成され、格納されます。 その後、そのプロパティにアクセスしようとすると、フォームのインスタンスが返されます。

フォームを破棄するには、そのフォームのプロパティに `Nothing` を割り当てます。 プロパティ セッターによって、フォームの <xref:System.Windows.Forms.Form.Close%2A> メソッドが呼び出され、格納されている値に `Nothing` が割り当てられます。 プロパティに `Nothing` 以外の値を割り当てた場合、セッターが <xref:System.ArgumentException> 例外をスローします。

`My.Forms` オブジェクトのプロパティにフォームのインスタンスが格納されているかどうかをテストするには、`Is` または `IsNot` 演算子を使用します。 これらの演算子を使用すると、プロパティの値が `Nothing` かどうかをチェックできます。

> [!NOTE]
> 通常、`Is` または `IsNot` 演算子では、比較を実行するためにプロパティの値を読み取る必要があります。 ただし、プロパティに現在 `Nothing` が格納されている場合は、プロパティによってフォームの新しいインスタンスが作成され、そのインスタンスが返されます。 ただし、Visual Basic コンパイラでは、`My.Forms` オブジェクトのプロパティが異なって処理されるため、`Is` または `IsNot` 演算子によって、値を変更せずにプロパティの状態をチェックできます。

## <a name="example"></a>例

この例では、既定の `SidebarMenu` フォームのタイトルを変更しています。

[!code-vb[VbVbalrMyForms#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyForms/VB/Class1.vb#2)]

この例を機能させるには、プロジェクトに `SidebarMenu` という名前のフォームが必要です。

このコードは、Windows アプリケーション プロジェクトでのみ機能します。

## <a name="requirements"></a>必要条件

### <a name="availability-by-project-type"></a>プロジェクトの種類別の可用性

|プロジェクトの種類|使用可能|
|---|---|
|Windows アプリケーション|**はい**|
|クラス ライブラリ|いいえ|
|コンソール アプリケーション|いいえ|
|Windows コントロール ライブラリ|いいえ|
|Web コントロール ライブラリ|いいえ|
|Windows サービス|いいえ|
|Web サイト|いいえ|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>
- <xref:System.Windows.Forms.Form>
- <xref:System.Windows.Forms.Form.Close%2A>
- [オブジェクト](index.md)
- [Is 演算子](../operators/is-operator.md)
- [IsNot 演算子](../operators/isnot-operator.md)
- [アプリケーション フォームへのアクセス](../../developing-apps/programming/accessing-application-forms.md)
