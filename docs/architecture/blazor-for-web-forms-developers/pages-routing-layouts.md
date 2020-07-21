---
title: ページ、ルーティング、レイアウト
description: でページを作成する方法 Blazor 、クライアント側のルーティングを使用する方法、およびページレイアウトを管理する方法について説明します。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 09/19/2019
ms.openlocfilehash: fc1f6f9420c7149b6e67123f2f68bef75667aa0c
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173108"
---
# <a name="pages-routing-and-layouts"></a>ページ、ルーティング、レイアウト

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

ASP.NET Web フォームアプリは、 *.aspx*ファイルで定義されたページで構成されます。 各ページのアドレスは、プロジェクトの物理ファイルパスに基づいています。 ブラウザーがページに要求を行うと、ページの内容がサーバーに動的に表示されます。 ページの HTML マークアップとそのサーバーコントロールの両方に対する表示アカウント。

で Blazor は、アプリの各ページは、通常、1つまたは複数の指定されたルートを使用して、razor ファイルで定義されているコンポーネントです *。* ルーティングは、ほとんどの場合、特定のサーバー要求を介さずにクライアント側で行われます。 ブラウザーはまず、アプリのルートアドレスに要求を行います。 `Router`その後、アプリ内のルートコンポーネントが、 Blazor 受信ナビゲーション要求を処理し、正しいコンポーネントに処理を行います。

Blazor*ディープリンク*もサポートします。 ディープリンクは、ブラウザーがアプリのルート以外の特定のルートに対して要求を行うときに発生します。 サーバーに送信されるディープリンクの要求はアプリにルーティングされ Blazor 、その後、要求のクライアント側が正しいコンポーネントにルーティングされます。

ASP.NET Web フォームの単純なページには、次のマークアップが含まれる場合があります。

*名前 .aspx*

```aspx-csharp
<%@ Page Title="Name" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Name.aspx.cs" Inherits="WebApplication1.Name" %>

<asp:Content ID="BodyContent" ContentPlaceHolderID="MainContent" runat="server">
    <div>
        What is your name?<br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
    </div>
    <div>
        <asp:Literal ID="Literal1" runat="server" />
    </div>
</asp:Content>
```

*Name.aspx.cs*

```csharp
public partial class Name : System.Web.UI.Page
{
    protected void Button1_Click1(object sender, EventArgs e)
    {
        Literal1.Text = "Hello " + TextBox1.Text;
    }
}
```

アプリの同等のページは次の Blazor ようになります。

*名前。 razor*

```razor
@page "/Name"
@layout MainLayout

<div>
    What is your name?<br />
    <input @bind="text" />
    <button @onclick="OnClick">Submit</button>
</div>
<div>
    @if (name != null)
    {
        @:Hello @name
    }
</div>

@code {
    string text;
    string name;

    void OnClick() {
        name = text;
    }
}
```

## <a name="create-pages"></a>ページの作成

でページを作成するには Blazor 、コンポーネントを作成し、Razor ディレクティブを追加して、 `@page` コンポーネントのルートを指定します。 ディレクティブは、 `@page` そのコンポーネントに追加するルートテンプレートである1つのパラメーターを受け取ります。

```razor
@page "/counter"
```

ルートテンプレートパラメーターが必要です。 ASP.NET Web フォームとは異なり、コンポーネントへのルートがファイルの場所から推論されることは Blazor あり*ません*(ただし、将来追加される機能である可能性があります)。

ルートテンプレートの構文は、ASP.NET Web フォームでのルーティングに使用される基本構文と同じです。 ルートパラメーターは、テンプレート内で中かっこを使用して指定されます。 Blazorルート値を同じ名前のコンポーネントパラメーターにバインドします (大文字と小文字は区別されません)。

```razor
@page "/product/{id}"

<h1>Product @Id</h1>

@code {
    [Parameter]
    public string Id { get; set; }
}
```

Route パラメーターの値に対して制約を指定することもできます。 たとえば、製品 ID をに制限するには、次のようにし `int` ます。

```razor
@page "/product/{id:int}"

<h1>Product @Id</h1>

@code {
    [Parameter]
    public int Id { get; set; }
}
```

でサポートされているルート制約の完全な一覧につい Blazor ては、「[ルート制約](/aspnet/core/blazor/routing#route-constraints)」を参照してください。

## <a name="router-component"></a>ルーターコンポーネント

でのルーティング Blazor は、コンポーネントによって処理され `Router` ます。 コンポーネントは、 `Router` 通常、アプリのルートコンポーネント (*app.xaml*) で使用されます。

```razor
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(MainLayout)">
            <p>Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```

コンポーネントは、指定されたでルーティング可能なコンポーネントを検出し、 `Router` 必要に `AppAssembly` 応じて指定 `AdditionalAssemblies` します。 ブラウザーが移動すると、はナビゲーションをインターセプトし、ルートがアドレスと一致する場合は抽出されたを `Router` 使用してパラメーターの内容をレンダリングし `Found` `RouteData` ます。それ以外の場合は、 `Router` パラメーターをレンダリングし `NotFound` ます。

`RouteView`コンポーネントは、によって指定された一致するコンポーネントを `RouteData` レイアウトと共に表示します (ある場合)。 一致したコンポーネントにレイアウトがない場合は、必要に応じて指定したが `DefaultLayout` 使用されます。

コンポーネントは、 `LayoutView` 指定されたレイアウト内で子コンテンツをレンダリングします。 レイアウトについては、この章で後ほど詳しく説明します。

## <a name="navigation"></a>ナビゲーション

ASP.NET Web フォームでは、ブラウザーにリダイレクト応答を返すことによって、別のページへのナビゲーションをトリガーします。 次に例を示します。

```csharp
protected void NavigateButton_Click(object sender, EventArgs e)
{
    Response.Redirect("Counter");
}
```

では、通常、リダイレクト応答を返すことはできません Blazor 。 Blazorでは、要求/応答モデルは使用されません。 ただし、JavaScript の場合と同様に、ブラウザーのナビゲーションを直接トリガーできます。

Blazorには、 `NavigationManager` 次のために使用できるサービスが用意されています。

- 現在のブラウザーアドレスを取得します
- ベースアドレスを取得する
- ナビゲーションのトリガー
- アドレスが変更されたときに通知を受け取る

別のアドレスに移動するには、メソッドを使用し `NavigateTo` ます。

```razor
@page "/"
@inject NavigationManager NavigationManager

<button @onclick="Navigate">Navigate</button>

@code {
    void Navigate() {
        NavigationManager.NavigateTo("counter");
    }
}
```

すべてのメンバーの説明につい `NavigationManager` ては、「 [URI およびナビゲーション状態ヘルパー](/aspnet/core/blazor/routing#uri-and-navigation-state-helpers)」を参照してください。

## <a name="base-urls"></a>ベース URL

Blazorアプリが基本パスの下にデプロイされている場合は、[作業にルーティング] プロパティを使用して、ページメタデータにベース URL を指定する必要があり `<base>` ます。 アプリケーションのホストページが Razor を使用してサーバーでレンダリングされる場合は、構文を使用して `~/` アプリのベースアドレスを指定できます。 ホストページが静的な HTML の場合は、ベース URL を明示的に指定する必要があります。

```html
<base href="~/" />
```

## <a name="page-layout"></a>ページのレイアウト

ASP.NET Web フォームのページレイアウトは、マスターページによって処理されます。 マスターページは、1つまたは複数のコンテンツのプレースホルダーを持つテンプレートを定義します。このプレースホルダーは、個々のページで提供できます。 マスターページは、 *.master*ファイルで定義され、ディレクティブで始まります `<%@ Master %>` 。 *.Master*ファイルの内容は *.aspx*ページと同じようにコード化されますが、 `<asp:ContentPlaceHolder>` ページがコンテンツを提供できる場所をマークするためのコントロールが追加されています。

*Site.master*

```aspx-csharp
<%@ Master Language="C#" AutoEventWireup="true" CodeBehind="Site.master.cs" Inherits="WebApplication1.SiteMaster" %>

<!DOCTYPE html>
<html lang="en">
<head runat="server">
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><%: Page.Title %> - My ASP.NET Application</title>
    <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
</head>
<body>
    <form runat="server">
        <div class="container body-content">
            <asp:ContentPlaceHolder ID="MainContent" runat="server">
            </asp:ContentPlaceHolder>
            <hr />
            <footer>
                <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
            </footer>
        </div>
    </form>
</body>
</html>
```

で Blazor は、レイアウトコンポーネントを使用してページレイアウトを処理します。 レイアウトコンポーネントはを継承 `LayoutComponentBase` します。これは、 `Body` `RenderFragment` ページの内容を表示するために使用できる型の単一のプロパティを定義します。

*MainLayout。 razor*

```razor
@inherits LayoutComponentBase
<h1>Main layout</h1>
<div>
    @Body
</div>
```

レイアウトが指定されたページが表示されると、レイアウトがプロパティをレンダリングする場所で、指定されたレイアウトの内容内にページがレンダリングされ `Body` ます。

ページにレイアウトを適用するには、ディレクティブを使用し `@layout` ます。

```razor
@layout MainLayout
```

*_Imports の razor*ファイルを使用して、フォルダーおよびサブフォルダー内のすべてのコンポーネントのレイアウトを指定できます。 [ルーターコンポーネント](#router-component)を使用して、すべてのページの既定のレイアウトを指定することもできます。

マスターページでは複数のコンテンツプレースホルダーを定義できますが、のレイアウトには Blazor 1 つのプロパティしかありません `Body` 。 レイアウトコンポーネントのこの制限 Blazor は、今後のリリースで対処される予定です。

ASP.NET Web フォームのマスターページは入れ子にすることができます。 つまり、マスターページでマスターページを使用することもできます。 のレイアウトコンポーネント Blazor も入れ子にすることができます。 レイアウトコンポーネントをレイアウトコンポーネントに適用できます。 内部レイアウトの内容は、外側のレイアウト内にレンダリングされます。

*ChildLayout。 razor*

```razor
@layout MainLayout
<h2>Child layout</h2>
<div>
    @Body
</div>
```

*インデックス。 razor*

```razor
@page "/"
@layout ChildLayout
<p>I'm in a nested layout!</p>
```

ページのレンダリングされた出力は次のようになります。

```html
<h1>Main layout</h1>
<div>
    <h2>Child layout</h2>
    <div>
        <p>I'm in a nested layout!</p>
    </div>
</div>
```

のレイアウトで Blazor は、通常、ページ (、、 `<html>` `<body>` など) のルート `<head>` HTML 要素は定義されません。 ルート HTML 要素は Blazor アプリのホストページで定義され、アプリの初期 html コンテンツを表示するために使用されます ( [「 Blazor ブートストラップ](project-structure.md#bootstrap-blazor)」を参照してください)。 ホストページでは、周囲のマークアップを含むアプリの複数のルートコンポーネントをレンダリングできます。

ページを Blazor 含め、のコンポーネントはタグをレンダリングできません `<script>` 。 `<script>`タグが一度読み込まれてから変更できないため、この表示制限が存在します。 Razor 構文を使用してタグを動的に表示しようとすると、予期しない動作が発生することがあります。 代わりに、すべての `<script>` タグをアプリのホストページに追加する必要があります。

>[!div class="step-by-step"]
>[前へ](components.md)
>[次へ](state-management.md)
