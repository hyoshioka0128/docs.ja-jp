---
title: データアクセスと管理
description: ASP.NET Web フォームおよびでデータにアクセスして処理する方法について説明し Blazor ます。
author: csharpfritz
ms.author: jefritz
no-loc:
- Blazor
ms.date: 04/26/2020
ms.openlocfilehash: 4bf9bee21ce1db828dbe0aeb156d5e15cae4f703
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173305"
---
# <a name="work-with-data"></a>データの処理

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

データアクセスは、ASP.NET Web フォームアプリのバックボーンです。 Web 用のフォームを構築している場合、そのデータはどうなりますか。 Web フォームでは、データベースの操作に使用できるデータアクセス手法が複数ありました。

- Data Sources
- ADO.NET
- Entity Framework

データソースは、Web フォームページ上に配置し、他のコントロールと同様に構成できるコントロールでした。 Visual Studio には、コントロールを構成して Web フォームページにバインドするための一連のダイアログボックスが用意されています。 "低コード" または "コードなし" のアプローチを利用している開発者は、Web フォームが最初にリリースされたときにこの手法を使用することをお勧めします。

![Data Sources](media/data/datasources.png)

ADO.NET は、データベースと対話するための低レベルのアプローチです。 アプリでは、操作のためのコマンド、レコードセット、およびデータセットを使用してデータベースへの接続を作成できます。 結果は、コードを記述せずに画面上のフィールドにバインドすることができます。 この方法の欠点は、ADO.NET オブジェクト (、、および) の各セットが、 `Connection` `Command` `Recordset` データベースベンダーによって提供されるライブラリにバインドされていることでした。 これらのコンポーネントを使用すると、コードが固定され、別のデータベースへの移行が困難になります。

## <a name="entity-framework"></a>Entity Framework

Entity Framework (EF) は、.NET Foundation によって管理されるオープンソースのオブジェクトリレーショナルマッピングフレームワークです。 .NET Framework と共に最初にリリースされた EF では、データベース接続、ストレージスキーマ、および相互作用のコードを生成できます。 この抽象化により、アプリのビジネスルールに集中し、信頼されたデータベース管理者がデータベースを管理できるようになります。 .NET Core では、EF Core と呼ばれる更新バージョンの EF を使用できます。 EF Core は、コマンドラインツールを使用して使用できる一連のコマンドを使用して、コードとデータベースの間の対話を生成し、維持するのに役立ち `dotnet ef` ます。 データベースを操作するためのいくつかのサンプルを見てみましょう。

### <a name="ef-code-first"></a>EF Code First

データベースとの対話の構築を簡単に開始するには、操作するクラスオブジェクトから開始する方法があります。 EF には、クラスに適したデータベースコードを生成するためのツールが用意されています。 このアプローチは、"Code First" の開発と呼ばれます。 `Product`Microsoft SQL Server のようなリレーショナルデータベースに格納するサンプルストアアプリの場合は、次のクラスを考えてみます。

```csharp
public class Product
{
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }

    [MaxLength(4000)]
    public string Description { get; set; }

    [Range(0, 99999,99)]
    [DataType(DataType.Currency)]
    public decimal Price { get; set; }
}
```

製品には主キーと、データベースに作成される3つの追加フィールドがあります。  

- EF では、 `Id` 規則によってプロパティが主キーとして識別されます。
- `Name`は、テキストストレージ用に構成された列に格納されます。 `[Required]`このプロパティを装飾する属性は、 `not null` プロパティのこの宣言された動作を強制するための制約を追加します。
- `Description`は、テキストストレージ用に構成された列に格納され、最大長は属性で指定された4000文字に設定され `[MaxLength]` ます。 データベーススキーマは、 `MaxLength` データ型を使用してという名前の列で構成され `varchar(4000)` ます。
- `Price`プロパティは通貨として格納されます。 属性は、 `[Range]` 宣言された最小値と最大値の範囲外のデータストレージを防ぐために、適切な制約を生成します。

この `Product` クラスは、データベースでの接続操作と変換操作を定義するデータベースコンテキストクラスに追加する必要があります。

```csharp
public class MyDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

クラスには、 `MyDbContext` クラスのアクセスと変換を定義する1つのプロパティが用意されて `Product` います。  アプリケーションでは、クラスのメソッドの次のエントリを使用して、データベースとの対話のためにこのクラスを構成し `Startup` `ConfigureServices` ます。

```csharp
services.AddDbContext<MyDbContext>(options =>
    options.UseSqlServer("MY DATABASE CONNECTION STRING"));
```

上記のコードは、指定された接続文字列を使用して SQL Server データベースに接続します。 appsettings.jsの接続文字列を、ファイル、環境変数、またはその他の構成ストレージの場所に配置し、この埋め込み文字列を適切*に*置き換えることができます。

その後、次のコマンドを使用して、このクラスに適したデータベーステーブルを生成できます。

```dotnetcli
dotnet ef migrations add 'Create Product table'
dotnet ef database update
```

最初のコマンドは、という新しい EF 移行として、データベーススキーマに対して行っている変更を定義し `Create Product table` ます。  移行では、新しいデータベースの変更を適用および削除する方法を定義します。

適用すると、データベースの単純な `Product` テーブルと、データベーススキーマの管理に役立つ新しいクラスがプロジェクトに追加されます。  これらの生成されたクラスは、既定では、*移行*という名前の新しいフォルダーにあります。  クラスに変更を加え `Product` たり、データベースと対話する関連クラスを追加したりする場合は、移行の新しい名前を指定してコマンドラインコマンドを再度実行する必要があります。  このコマンドでは、データベーススキーマを更新するために別の一連の移行クラスが生成されます。

### <a name="ef-database-first"></a>EF Database First

既存のデータベースの場合は、.NET コマンドラインツールを使用して EF Core のクラスを生成できます。 クラスをスキャフォールディングするには、次のコマンドのバリエーションを使用します。

```dotnetcli
dotnet ef dbcontext scaffold "CONNECTION STRING" Microsoft.EntityFrameworkCore.SqlServer -c MyDbContext -t Product -t Customer
```

上記のコマンドは、指定された接続文字列とプロバイダーを使用してデータベースに接続し `Microsoft.EntityFrameworkCore.SqlServer` ます。 接続されると、という名前のデータベースコンテキストクラス `MyDbContext` が作成されます。 また、 `Product` オプションで指定されたテーブルおよびテーブルに対してサポートクラスが作成され `Customer` `-t` ます。 このコマンドには、データベースに適したクラス階層を生成するための多くの構成オプションがあります。 完全なリファレンスについては、[コマンドのドキュメント](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-dbcontext-scaffold)を参照してください。

[EF Core](/ef/core/)の詳細については、Microsoft Docs サイトを参照してください。

## <a name="interact-with-web-services"></a>Web サービスとの対話

ASP.NET が最初にリリースされたときに、web サーバーとクライアントがデータを交換するために、SOAP サービスが推奨されていました。 その後、多くの変更が行われ、HTTP クライアントとの対話を直接行うためにサービスとの優先的なやり取りが行われています。 と ASP.NET Core を使用 Blazor すると、 `HttpClient` クラスのメソッドにの構成を登録でき `Startup` `ConfigureServices` ます。 HTTP エンドポイントと対話する必要がある場合は、その構成を使用します。 次の構成コードを考えてみます。

```csharp
services.AddHttpClient("github", client =>
{
    client.BaseAddress = new Uri("http://api.github.com/");
    // Github API versioning
    client.DefaultRequestHeaders.Add("Accept", "application/vnd.github.v3+json");
    // Github requires a user-agent
    client.DefaultRequestHeaders.Add("User-Agent", "BlazorWebForms-Sample");
});
```

GitHub からデータにアクセスする必要がある場合は常に、という名前のクライアントを作成 `github` します。 クライアントはベースアドレスを使用して構成され、要求ヘッダーが適切に設定されます。 `IHttpClientFactory` Blazor ディレクティブまたはプロパティの属性を使用して、をコンポーネントに挿入し `@inject` `[Inject]` ます。 次の構文を使用して、名前付きクライアントを作成し、サービスと対話します。

```razor
@inject IHttpClientFactory factory

...

@code {
    protected override async Task OnInitializedAsync()
    {
        var client = factory.CreateClient("github");
        var response = await client.GetAsync("repos/dotnet/docs/issues");
        response.EnsureStatusCode();
        var content = async response.Content.ReadAsStringAsync();
    }
}
```

このメソッドは、 *dotnet/docs* GitHub リポジトリ内の問題のコレクションを記述する文字列を返します。 JSON 形式でコンテンツを返し、適切な GitHub issue オブジェクトに逆シリアル化されます。 事前に構成されたオブジェクトを配信するようにを構成するには、さまざまな方法があり `HttpClientFactory` `HttpClient` ます。 使用 `HttpClient` するさまざまな web サービスに対して、異なる名前とエンドポイントで複数のインスタンスを構成してみてください。 この方法では、これらのサービスとのやり取りを、各ページで簡単に操作できるようにします。 詳細については、 [IHttpClientFactory のドキュメント](/aspnet/core/fundamentals/http-requests)を参照してください。

>[!div class="step-by-step"]
>[前へ](forms-validation.md)
>[次へ](middleware.md)
