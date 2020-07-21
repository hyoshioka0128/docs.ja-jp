---
title: を使用して再利用可能な UI コンポーネントを構築するBlazor
description: を使用して再利用可能な UI コンポーネントを構築する方法 Blazor と、それらを ASP.NET Web フォームコントロールと比較する方法について説明します。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 09/18/2019
ms.openlocfilehash: 9577fc916bb11783b885b2641242820865c0b115
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173342"
---
# <a name="build-reusable-ui-components-with-blazor"></a>を使用して再利用可能な UI コンポーネントを構築するBlazor

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

ASP.NET Web フォームに関するすばらしい点の1つは、再利用可能なユーザーインターフェイス (UI) コードを再利用可能な UI コントロールにカプセル化できるようにする方法です。 カスタムユーザーコントロールは、 *.ascx*ファイルを使用してマークアップで定義できます。 デザイナーを完全にサポートするコードで、複雑なサーバーコントロールを作成することもできます。

Blazorでは、*コンポーネント*による UI カプセル化もサポートされています。 コンポーネント:

- は、UI の自己完結型のチャンクです。
- は、独自の状態およびレンダリングロジックを保持します。
- UI イベントハンドラーを定義し、入力データにバインドして、独自のライフサイクルを管理できます。
- は、通常、Razor 構文を使用する*razor*ファイルで定義されます。

## <a name="an-introduction-to-razor"></a>Razor の概要

Razor は、HTML および C# に基づく軽量のマークアップテンプレート言語です。 Razor を使用すると、マークアップと C# のコードをシームレスに切り替えて、コンポーネントのレンダリングロジックを定義できます。 *Razor*ファイルがコンパイルされると、レンダリングロジックは .net クラスで構造化された方法でキャプチャされます。 コンパイル済みクラスの名前は、 *razor*ファイル名から取得されます。 名前空間は、プロジェクトの既定の名前空間およびフォルダーパスから取得されます。また、ディレクティブを使用して名前空間を明示的に指定することもでき `@namespace` ます (以下の Razor ディレクティブについてはこちらを参照してください)。

コンポーネントのレンダリングロジックは、C# を使用して動的なロジックが追加された通常の HTML マークアップを使用して作成されます。 `@`文字は、C# に移行するために使用されます。 Razor は、通常、HTML に切り替えたときに理解することが賢明です。 たとえば、次のコンポーネントは、 `<p>` 現在の時刻を使用してタグをレンダリングします。

```razor
<p>@DateTime.Now</p>
```

C# 式の開始と終了を明示的に指定するには、かっこを使用します。

```razor
<p>@(DateTime.Now)</p>
```

Razor では、レンダリングロジックで C# の制御フローを簡単に使用することもできます。 たとえば、次のような HTML を条件付きでレンダリングできます。

```razor
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

または、次のような通常の C# ループを使用して項目の一覧を生成することもでき `foreach` ます。

```razor
<ul>
@foreach (var item in items)
{
    <li>@item.Text</li>
}
</ul>
```

Razor ディレクティブは、ASP.NET Web フォームのディレクティブと同様に、Razor コンポーネントのコンパイル方法の多くの側面を制御します。 コンポーネントの例を次に示します。

- 名前空間
- 基底クラス
- 実装されたインターフェイス
- ジェネリックパラメーター
- [インポートされた名前空間]
- ルート

Razor ディレクティブは、文字で始まり、 `@` 通常、ファイルの先頭にある新しい行の先頭で使用されます。 たとえば、ディレクティブは `@namespace` コンポーネントの名前空間を定義します。

```razor
@namespace MyComponentNamespace
```

次の表は、で使用されるさまざまな Razor ディレクティブ Blazor と、それらが存在する場合の ASP.NET Web フォームに相当するものをまとめたものです。

|ディレクティブ    |説明|例|同等の Web フォーム|
|-------------|-----------|-------|--------------------|
|`@attribute` |コンポーネントにクラスレベルの属性を追加します。|`@attribute [Authorize]`|なし|
|`@code`      |コンポーネントにクラスメンバーを追加します。|`@code { ... }`|`<script runat="server">...</script>`|
|`@implements`|指定したインターフェイスを実装します。|`@implements IDisposable`|コードビハインドを使用する|
|`@inherits`  |指定した基底クラスから継承します。|`@inherits MyComponentBase`|`<%@ Control Inherits="MyUserControlBase" %>`|
|`@inject`    |コンポーネントにサービスを挿入します。|`@inject IJSRuntime JS`|なし|
|`@layout`    |コンポーネントのレイアウトコンポーネントを指定します。|`@layout MainLayout`|`<%@ Page MasterPageFile="~/Site.Master" %>`|
|`@namespace` |コンポーネントの名前空間を設定します。|`@namespace MyNamespace`|なし|
|`@page`      |コンポーネントのルートを指定します。|`@page "/product/{id}"`|`<%@ Page %>`|
|`@typeparam` |コンポーネントのジェネリック型パラメーターを指定します。|`@typeparam TItem`|コードビハインドを使用する|
|`@using`     |スコープに取り込む名前空間を指定します|`@using MyComponentNamespace`|*web.config*に名前空間を追加する|

また、Razor コンポーネントでは、要素に対して*ディレクティブ属性*を広範に使用して、コンポーネントのコンパイル (イベント処理、データバインディング、コンポーネント & 要素参照など) のさまざまな側面を制御します。 ディレクティブ属性は、かっこ内の値が省略可能である一般的なジェネリック構文に従います。

```razor
@directive(-suffix(:name))(="value")
```

次の表は、で使用される Razor ディレクティブのさまざまな属性をまとめたもの Blazor です。

|属性    |[説明]|例|
|-------------|-----------|-------|
|`@attributes`|属性のディクショナリをレンダリングします|`<input @attributes="ExtraAttributes" />`|
|`@bind`      |双方向のデータバインディングを作成します。    |`<input @bind="username" @bind:event="oninput" />`|
|`@on{event}` |指定したイベントのイベントハンドラーを追加します。|`<button @onclick="IncrementCount">Click me!</button>`|
|`@key`       |コレクション内の要素を保持するために比較アルゴリズムによって使用されるキーを指定します。|`<DetailsEditor @key="person" Details="person.Details" />`|
|`@ref`       |コンポーネントまたは HTML 要素への参照をキャプチャします。|`<MyDialog @ref="myDialog" />`|

で使用されるさまざまなディレクティブ属性 Blazor ( `@onclick` 、 `@bind` 、 `@ref` など) については、以降の章で説明します。

*.Aspx*および *.ascx*ファイルで使用される構文の多くには、Razor の並列構文があります。 次に、ASP.NET Web フォームと Razor の構文を簡単に比較します。

|機能                      |Web フォーム           |構文               |Razor         |構文 |
|-----------------------------|--------------------|---------------------|--------------|-------|
|ディレクティブ                   |`<%@ [directive] %>`|`<%@ Page %>`        |`@[directive]`|`@page`|
|コード ブロック                  |`<% %>`             |`<% int x = 123; %>` |`@{ }`        |`@{ int x = 123; }`|
|式<br>(HTML エンコード)|`<%: %>`            |`<%:DateTime.Now %>` |順序`@`<br>順序`@()`|`@DateTime.Now`<br>`@(DateTime.Now)`|
|コメント                     |`<%-- --%>`         |`<%-- Commented --%>`|`@* *@`       |`@* Commented *@`|
|データ バインディング                 |`<%# %>`            |`<%# Bind("Name") %>`|`@bind`       |`<input @bind="username" />`|

Razor コンポーネントクラスにメンバーを追加するには、ディレクティブを使用し `@code` ます。 この手法は、 `<script runat="server">...</script>` ASP.NET Web フォームのユーザーコントロールまたはページでブロックを使用するのと似ています。

```razor
@code {
    int count = 0;

    void IncrementCount()
    {
        count++;
    }
}
```

Razor は c# に基づいているため、C# プロジェクト (*.csproj*) 内からコンパイルする必要があります。 Visual Basic プロジェクト (*.vbproj*) から*razor*ファイルをコンパイルすることはできません。 プロジェクトから Visual Basic プロジェクトを参照することもでき Blazor ます。 逆も同様です。

完全 Razor 構文リファレンスについては、「 [ASP.NET Core の Razor 構文リファレンス](/aspnet/core/mvc/views/razor)」を参照してください。

## <a name="use-components"></a>コンポーネントを使う

通常の HTML とは別に、コンポーネントはレンダリングロジックの一部として他のコンポーネントを使用することもできます。 Razor でコンポーネントを使用するための構文は、ASP.NET Web フォームアプリでユーザーコントロールを使用する場合と似ています。 コンポーネントは、コンポーネントの型名と一致する要素タグを使用して指定されます。 たとえば、次の `Counter` ようなコンポーネントを追加できます。

```razor
<Counter />
```

ASP.NET Web フォームとは異なり、のコンポーネントは Blazor 次のとおりです。

- 要素のプレフィックスは使用しないでください (たとえば、 `asp:` )。
- ページまたは*web.config*での登録は必要ありません。

.NET 型のような Razor コンポーネントについて考えてみましょう。これはまさにそのようなものです。 コンポーネントを含むアセンブリが参照されている場合は、コンポーネントを使用できます。 コンポーネントの名前空間をスコープに入れるには、ディレクティブを適用し `@using` ます。

```razor
@using MyComponentLib

<Counter />
```

既定のプロジェクトに示されているように Blazor 、ディレクティブを _Imports の razor ファイルに配置するのが一般的です。 `@using` これにより、同じディレクトリおよび子ディレクトリ内のすべての*razor*ファイルにディレクティブがインポート *_Imports.razor*されます。

コンポーネントの名前空間がスコープ内にない場合は、C# の場合と同様に、完全な型名を使用してコンポーネントを指定できます。

```razor
<MyComponentLib.Counter />
```

## <a name="component-parameters"></a>コンポーネントのパラメーター

ASP.NET Web フォームでは、パブリックプロパティを使用して、パラメーターとデータをコントロールにフローできます。 これらのプロパティは、属性を使用してマークアップで設定することも、コードで直接設定することもできます。 Blazorコンポーネントのプロパティは、コンポーネントのパラメーターと見なされるように属性でマークする必要もありますが、同様の方法で動作し `[Parameter]` ます。

次のコンポーネントでは、 `Counter` `IncrementAmount` ボタンがクリックされるたびにがインクリメントされる量を指定するために使用できる、というコンポーネントパラメーターを定義して `Counter` います。

```razor
<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    int currentCount = 0;

    [Parameter]
    public int IncrementAmount { get; set; } = 1;

    void IncrementCount()
    {
        currentCount+=IncrementAmount;
    }
}
```

でコンポーネントパラメーターを指定するに Blazor は、ASP.NET Web フォームの場合と同じように属性を使用します。

```razor
<Counter IncrementAmount="10" />
```

## <a name="event-handlers"></a>イベント ハンドラー

ASP.NET Web フォームとはどちらも、 Blazor UI イベントを処理するためのイベントベースのプログラミングモデルを提供します。 このようなイベントの例としては、ボタンのクリックやテキスト入力などがあります。 ASP.NET Web フォームでは、HTML サーバーコントロールを使用して、DOM によって公開される UI イベントを処理したり、web サーバーコントロールによって公開されるイベントを処理したりすることができます。 イベントは、ポストバック要求のフォームを使用してサーバー上に表示されます。 次の Web フォームのボタンをクリックする例を考えてみましょう。

*カウンタ .ascx*

```aspx-csharp
<asp:Button ID="ClickMeButton" runat="server" Text="Click me!" OnClick="ClickMeButton_Click" />
```

*Counter.ascx.cs*

```csharp
public partial class Counter : System.Web.UI.UserControl
{
    protected void ClickMeButton_Click(object sender, EventArgs e)
    {
        Console.WriteLine("The button was clicked!");
    }
}
```

では Blazor 、フォームのディレクティブ属性を使用して、DOM UI イベントのハンドラーを直接登録でき `@on{event}` ます。 プレースホルダーは、 `{event}` イベントの名前を表します。 たとえば、次のようなボタンのクリックをリッスンできます。

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    void OnClick()
    {
        Console.WriteLine("The button was clicked!);
    }
}
```

イベントハンドラーは、イベントに関する詳細情報を提供するために、省略可能なイベント固有の引数を受け取ることができます。 たとえば、マウスイベントは引数を受け取ることができますが、必須ではありません `MouseEventArgs` 。

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    void OnClick(MouseEventArgs e)
    {
        Console.WriteLine($"Mouse clicked at {e.ScreenX}, {e.ScreenY}.");
    }
}
```

イベントハンドラーのメソッドグループを参照する代わりに、ラムダ式を使用できます。 ラムダ式を使用すると、他のスコープ内の値を閉じることができます。

```razor
@foreach (var buttonLabel in buttonLabels)
{
    <button @onclick="() => Console.WriteLine($"The {buttonLabel} button was clicked!")">@buttonLabel</button>
}
```

イベントハンドラーは、同期または非同期で実行できます。 たとえば、次の `OnClick` イベントハンドラーは非同期的に実行されます。

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    async Task OnClick()
    {
        var result = await Http.GetAsync("api/values");
    }
}
```

イベントが処理されると、コンポーネントは、コンポーネントの状態の変更を考慮してレンダリングされます。 非同期イベントハンドラーを使用すると、ハンドラーの実行が完了した直後にコンポーネントがレンダリングされます。 非同期の完了後に、コンポーネントが*再び*表示され `Task` ます。 この非同期実行モードでは、非同期の処理中に適切な UI を表示することが `Task` できます。

```razor
<button @onclick="ShowMessage">Get message</button>

@if (showMessage)
{
    @if (message == null)
    {
        <p><em>Loading...</em></p>
    }
    else
    {
        <p>The message is: @message</p>
    }
}

@code
{
    bool showMessage = false;
    string message;

    public async Task ShowMessage()
    {
        showMessage = true;
        message = await MessageService.GetMessageAsync();
    }
}
```

コンポーネントは、型のコンポーネントパラメーターを定義することで、独自のイベントを定義することもでき `EventCallback<TValue>` ます。 イベントコールバックは、省略可能な引数、同期または非同期、メソッドグループ、ラムダ式など、DOM UI イベントハンドラーのすべてのバリエーションをサポートします。

```razor
<button class="btn btn-primary" @onclick="OnClick">Click me!</button>

@code {
    [Parameter]
    public EventCallback<MouseEventArgs> OnClick { get; set; }
}
```

## <a name="data-binding"></a>データ バインディング

BlazorUI コンポーネントのデータをコンポーネントの状態にバインドするための単純なメカニズムを提供します。 この方法は、データソースから UI コントロールにデータをバインドするための ASP.NET Web フォームの機能とは異なります。 データの処理に[関する](data.md)セクションでは、さまざまなデータソースからのデータの処理について説明します。

UI コンポーネントからコンポーネントの状態への双方向のデータバインディングを作成するには、ディレクティブ属性を使用し `@bind` ます。 次の例では、チェックボックスの値がフィールドにバインドされてい `isChecked` ます。

```razor
<input type="checkbox" @bind="isChecked" />

@code {
    bool isChecked;
}
```

コンポーネントがレンダリングされると、チェックボックスの値がフィールドの値に設定され `isChecked` ます。 ユーザーがチェックボックスをオンにすると、 `onchange` イベントが発生し、 `isChecked` フィールドが新しい値に設定されます。 `@bind`この場合の構文は、次のマークアップに相当します。

```razor
<input value="@isChecked" @onchange="(UIChangeEventArgs e) => isChecked = e.Value" />
```

バインドに使用するイベントを変更するには、属性を使用し `@bind:event` ます。

```razor
<input @bind="text" @bind:event="oninput" />
<p>@text</p>

@code {
    string text;
}
```

コンポーネントは、パラメーターへのデータバインディングをサポートすることもできます。 データバインドには、バインド可能なパラメーターと同じ名前のイベントコールバックパラメーターを定義します。 "Changed" サフィックスが名前に追加されます。

*PasswordBox。 razor*

```razor
Password: <input
    value="@Password"
    @oninput="OnPasswordChanged"
    type="@(showPassword ? "text" : "password")" />

<label><input type="checkbox" @bind="showPassword" />Show password</label>

@code {
    private bool showPassword;

    [Parameter]
    public string Password { get; set; }

    [Parameter]
    public EventCallback<string> PasswordChanged { get; set; }

    private Task OnPasswordChanged(ChangeEventArgs e)
    {
        Password = e.Value.ToString();
        return PasswordChanged.InvokeAsync(Password);
    }
}
```

データバインディングを基になる UI 要素に連結するには、属性を使用するのではなく、値を設定し、UI 要素のイベントを直接処理し `@bind` ます。

コンポーネントパラメーターにバインドするには、属性を使用して、バインド先の `@bind-{Parameter}` パラメーターを指定します。

```razor
<PasswordBox @bind-Password="password" />

@code {
    string password;
}
```

## <a name="state-changes"></a>状態変更

コンポーネントの状態が通常の UI イベントまたはイベントコールバックの外部で変更された場合、コンポーネントは、再レンダリングが必要であることを手動で通知する必要があります。 コンポーネントの状態が変更されたことを通知するには、 `StateHasChanged` コンポーネントでメソッドを呼び出します。

次の例では、コンポーネントに `AppState` よって、アプリの他の部分で更新可能なサービスからのメッセージが表示されます。 コンポーネントは、 `StateHasChanged` `AppState.OnChange` メッセージが更新されるたびにコンポーネントがレンダリングされるように、そのメソッドをイベントに登録します。

```csharp
public class AppState
{
    public string Message { get; }

    // Lets components receive change notifications
    public event Action OnChange;

    public void UpdateMessage(string message)
    {
        Message = message;
        NotifyStateChanged();
    }

    private void NotifyStateChanged() => OnChange?.Invoke();
}
```

```razor
@inject AppState AppState

<p>App message: @AppState.Message</p>

@code {
    protected override void OnInitialized()
    {
        AppState.OnChange += StateHasChanged
    }
}
```

## <a name="component-lifecycle"></a>コンポーネントのライフサイクル

ASP.NET Web Forms framework には、モジュール、ページ、およびコントロールに対して明確に定義されたライフサイクルメソッドがあります。 たとえば、次のコントロールは `Init` 、、、およびの各 `Load` ライフサイクルイベントのイベントハンドラーを実装し `UnLoad` ます。

*Counter.ascx.cs*

```csharp
public partial class Counter : System.Web.UI.UserControl
{
    protected void Page_Init(object sender, EventArgs e) { ... }
    protected void Page_Load(object sender, EventArgs e) { ... }
    protected void Page_UnLoad(object sender, EventArgs e) { ... }
}
```

Blazorコンポーネントには、明確に定義されたライフサイクルもあります。 コンポーネントのライフサイクルは、コンポーネントの状態を初期化し、高度なコンポーネントの動作を実装するために使用できます。

のすべての Blazor コンポーネントライフサイクルメソッドには、同期バージョンと非同期バージョンの両方があります。 コンポーネントのレンダリングは同期です。 コンポーネントレンダリングの一部として非同期ロジックを実行することはできません。 すべての非同期ロジックは、ライフサイクルメソッドの一部として実行する必要があり `async` ます。

### <a name="oninitialized"></a>OnInitialized 化

`OnInitialized`コンポーネントを `OnInitializedAsync` 初期化するには、メソッドとメソッドを使用します。 コンポーネントは通常、最初のレンダリング後に初期化されます。 コンポーネントが初期化されると、最終的に破棄される前に複数回レンダリングされる可能性があります。 `OnInitialized`メソッドは、 `Page_Load` ASP.NET Web フォームのページおよびコントロールのイベントに似ています。

```csharp
protected override void OnInitialized() { ... }
protected override async Task OnInitializedAsync() { await ... }
```

### <a name="onparametersset"></a>OnParametersSet

`OnParametersSet`コンポーネントが `OnParametersSetAsync` 親からパラメーターを受け取り、値がプロパティに割り当てられるときに、メソッドとメソッドが呼び出されます。 これらのメソッドは、コンポーネントの初期化の後、および*コンポーネントがレンダリング*されるたびに実行されます。

```csharp
protected override void OnParametersSet() { ... }
protected override async Task OnParametersSetAsync() { await ... }
```

### <a name="onafterrender"></a>OnAfterRender

`OnAfterRender`メソッドと `OnAfterRenderAsync` メソッドは、コンポーネントのレンダリングが完了した後に呼び出されます。 この時点で、要素参照とコンポーネント参照が設定されます (以下の概念を参照)。 この時点では、ブラウザーとの対話機能が有効になっています。 DOM および JavaScript の実行とのやり取りは、安全に実行できます。

```csharp
protected override void OnAfterRender(bool firstRender)
{
    if (firstRender)
    {
        ...
    }
}
protected override async Task OnAfterRenderAsync(bool firstRender)
{
    if (firstRender)
    {
        await ...
    }
}
```

`OnAfterRender``OnAfterRenderAsync`*サーバーでのプリレンダリング時には呼び出されませ*ん。

`firstRender`パラメーターは、 `true` コンポーネントが初めてレンダリングされるときに指定します。それ以外の場合は、値はに `false` なります。

### <a name="idisposable"></a>IDisposable

Blazorコンポーネント `IDisposable` が UI から削除されると、コンポーネントはを実装してリソースを破棄できます。 Razor コンポーネントは、ディレクティブを使用してを実装でき `IDispose` `@implements` ます。

```razor
@using System
@implements IDisposable

...

@code {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="capture-component-references"></a>コンポーネント参照のキャプチャ

ASP.NET Web フォームでは、ID を参照することによって、コントロールインスタンスをコード内で直接操作するのが一般的です。 では Blazor 、コンポーネントへの参照をキャプチャして操作することもできますが、これはあまり一般的ではありません。

でコンポーネント参照をキャプチャするには Blazor 、 `@ref` ディレクティブ属性を使用します。 属性の値は、参照されるコンポーネントと同じ型の設定可能フィールドの名前と一致している必要があります。

```razor
<MyLoginDialog @ref="loginDialog" ... />

@code {
    MyLoginDialog loginDialog;

    void OnSomething()
    {
        loginDialog.Show();
    }
}
```

親コンポーネントがレンダリングされると、そのフィールドに子コンポーネントインスタンスが設定されます。 その後、コンポーネントインスタンスのメソッドを呼び出したり、それ以外の操作を行ったりすることができます。

コンポーネント参照を使用してコンポーネントの状態を直接操作することは推奨されません。 これにより、コンポーネントが適切な時刻に自動的にレンダリングされるのを防ぐことができます。

## <a name="capture-element-references"></a>要素参照のキャプチャ

Blazorコンポーネントは、要素への参照をキャプチャできます。 ASP.NET Web フォームの HTML サーバーコントロールとは異なり、の要素参照を使用して DOM を直接操作することはできません Blazor 。 Blazordom 比較アルゴリズムを使用して、ほとんどの DOM 対話を処理します。 でキャプチャされた要素参照 Blazor は不透明です。 ただし、JavaScript の相互運用呼び出しで特定の要素参照を渡すために使用されます。 JavaScript の相互運用機能の詳細については、「 [ASP.NET Core Blazor javascript interop](/aspnet/core/blazor/javascript-interop)」を参照してください。

## <a name="templated-components"></a>テンプレート コンポーネント

ASP.NET Web フォームでは、テンプレート化された*コントロール*を作成できます。 開発者は、テンプレート化されたコントロールを使用して、コンテナーコントロールの表示に使用する HTML の一部を指定できます。 テンプレート化されたサーバーコントロールを構築するメカニズムは複雑ですが、ユーザーがカスタマイズ可能な方法でデータを表示するための強力なシナリオを実現します。 テンプレート化されたコントロールの例 `Repeater` として、やがあり `DataList` ます。

Blazorコンポーネントは、型または型のコンポーネントパラメーターを定義することによって、テンプレートを設定することもでき `RenderFragment` `RenderFragment<T>` ます。 は、 `RenderFragment` コンポーネントによってレンダリングできる Razor マークアップのチャンクを表します。 は、 `RenderFragment<T>` レンダリングフラグメントのレンダリング時に指定できるパラメーターを受け取る Razor マークアップのチャンクです。

### <a name="child-content"></a>子コンテンツ

Blazorコンポーネントは、子コンテンツをとしてキャプチャ `RenderFragment` し、コンポーネントレンダリングの一部としてそのコンテンツをレンダリングできます。 子コンテンツをキャプチャするには、型のコンポーネントパラメーターを定義 `RenderFragment` し、という名前を指定し `ChildContent` ます。

*ChildContentComponent。 razor*

```razor
<h1>Component with child content</h1>

<div>@ChildContent</div>

@code {
    [Parameter]
    public RenderFragment ChildContent { get; set; }
}
```

親コンポーネントは、通常の Razor 構文を使用して子コンテンツを提供できます。

```razor
<ChildContentComponent>
    <p>The time is @DateTime.Now</p>
</ChildContentComponent>
```

### <a name="template-parameters"></a>テンプレート パラメーター

また、テンプレート Blazor コンポーネントでは、型または型の複数のコンポーネントパラメーターを定義することもでき `RenderFragment` `RenderFragment<T>` ます。 のパラメーターは、 `RenderFragment<T>` 呼び出されたときに指定できます。 コンポーネントのジェネリック型パラメーターを指定するには、Razor ディレクティブを使用し `@typeparam` ます。

*SimpleListView。 razor*

```razor
@typeparam TItem

@Heading

<ul>
@foreach (var item in Items)
{
    <li>@ItemTemplate(item)</li>
}
</ul>

@code {
    [Parameter]
    public RenderFragment Heading { get; set; }

    [Parameter]
    public RenderFragment<TItem> ItemTemplate { get; set; }

    [Parameter]
    public IEnumerable<TItem> Items { get; set; }
}
```

テンプレート化されたコンポーネントを使用する場合、テンプレートパラメーターは、パラメーターの名前と一致する子要素を使用して指定できます。 `RenderFragment<T>`要素として渡される型のコンポーネント引数には、という名前の暗黙的なパラメーターがあり `context` ます。 子要素の属性を使用して、この実装パラメーターの名前を変更でき `Context` ます。 ジェネリック型パラメーターは、型パラメーターの名前と一致する属性を使用して指定できます。 可能な場合は、型パラメーターが推論されます。

```razor
<SimpleListView Items="messages" TItem="string">
    <Heading>
        <h1>My list</h1>
    </Heading>
    <ItemTemplate Context="message">
        <p>The message is: @message</p>
    </ItemTemplate>
</SimpleListView>
```

このコンポーネントの出力は次のようになります。

```html
<h1>My list</h1>
<ul>
    <li><p>The message is: message1</p></li>
    <li><p>The message is: message2</p></li>
<ul>
```

## <a name="code-behind"></a>分離コード

Blazorコンポーネントは通常、単一の*razor*ファイルで作成されます。 ただし、分離コードファイルを使用して、コードとマークアップを分離することもできます。 コンポーネントファイルを使用するには、コンポーネントファイルのファイル名と一致し、 *.cs*拡張子を追加した C# ファイルを追加します (*Counter.razor.cs*)。 コンポーネントの基本クラスを定義するには、C# ファイルを使用します。 基底クラスには任意の名前を指定できますが、クラスにはコンポーネントクラスと同じ名前を付けますが、 `Base` 拡張機能が追加され `CounterBase` ます ()。 コンポーネントベースのクラスも、から派生する必要があり `ComponentBase` ます。 次に、Razor コンポーネントファイルで、ディレクティブを追加して、 `@inherits` コンポーネントの基本クラスを指定し `@inherits CounterBase` ます ()。

*カウンタ。 razor*

```razor
@inherits CounterBase

<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button @onclick="IncrementCount">Click me</button>
```

*Counter.razor.cs*

```csharp
public class CounterBase : ComponentBase
{
    protected int currentCount = 0;

    protected void IncrementCount()
    {
        currentCount++;
    }
}
```

基底クラスのコンポーネントのメンバーの可視性は、 `protected` コンポーネントクラスに表示される必要があり `public` ます。

## <a name="additional-resources"></a>その他の技術情報

前のは、コンポーネントのすべての側面を網羅するものではありません Blazor 。 [ASP.NET Core Razor コンポーネントを作成して使用](/aspnet/core/blazor/components)する方法の詳細については、のドキュメントを参照してください Blazor 。

>[!div class="step-by-step"]
>[前へ](app-startup.md)
>[次へ](pages-routing-layouts.md)
