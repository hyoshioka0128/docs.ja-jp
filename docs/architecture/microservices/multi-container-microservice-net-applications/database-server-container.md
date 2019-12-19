---
title: コンテナーとして実行するデータベース サーバーの使用
description: コンテナー化された .NET アプリケーションの .NET マイクロサービス アーキテクチャ | 開発のためだけにコンテナーとして実行するデータベース サーバーを使用していますか。 理由を理解します。
ms.date: 10/02/2018
ms.openlocfilehash: 371d622dc39681edb0b52e723faccbf611b7797c
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74568431"
---
# <a name="using-a-database-server-running-as-a-container"></a>コンテナーとして実行するデータベース サーバーの使用

データベース (SQL Server、PostgreSQL、MySQL など) は、通常のスタンドアロン サーバー上、オンプレミス クラスター内、または Azure SQL DB などのクラウド内の PaaS サービスとして使用できます。 ただし、開発およびテスト環境では、データベースをコンテナーとして実行すると便利です。これは、外部の依存関係がなく、`docker-compose up` コマンドを実行するだけで、アプリケーション全体が起動するためです。 それらのデータベースをコンテナーとして使用することは、統合テストにも有効です。これは、データベースがコンテナー内で起動され、常に同じサンプル データが格納されるので、テストの予測精度が向上するためです。

### <a name="sql-server-running-as-a-container-with-a-microservice-related-database"></a>マイクロサービスに関連するデータベースを含むコンテナーとして実行している SQL Server

eShopOnContainers には、[docker-compose.yml](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/docker-compose.yml) ファイルで定義される sql.data というコンテナーがあり、これが Linux 用 SQL Server とマイクロサービスに必要なすべての SQL Server データベースを実行します (各データベース用に 1 つの SQL Server コンテナーを使用することもできますが、より多くのメモリを Docker に割り当てる必要があります)。マイクロサービスで重要な点は、各マイクロサービスが関連するデータを所有し、そのためこのケースでは、SQL データベースに関連付けられます。 しかし、データベースは任意の場所に置くことができます。

サンプル アプリケーションの SQL Server コンテナーは、docker-compose.yml ファイル内で次の YAML コードで構成され、`docker-compose up` を実行したときに実行されます。 YAML コードは、汎用の docker compose.yml ファイルと docker compose.override.yml ファイルから構成情報を統合されていることに注意してください (通常は、SQL Server イメージに関連する基本情報または静的情報から、環境の設定を分離します)。

```yml
  sql.data:
    image: microsoft/mssql-server-linux:2017-latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5434:1433"
```

同様の方法で、`docker-compose` を使用する代わりに、次の `docker run` コマンドでそのコンテナーを実行できます。

```console
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Pass@word' -p 5433:1433 -d microsoft/mssql-server-linux:2017-latest
```

ただし、eShopOnContainers などのマルチコンテナー アプリケーションを展開する場合は、アプリケーションに必要なすべてのコンテナーを展開する `docker-compose up` コマンドを使う方が便利です。

初めてこの SQL Server のコンテナーを起動するときに、コンテナーが、指定したパスワードを使用して SQL Server を初期化します。 SQL Server がコンテナーとして実行されたら、SQL Server Management Studio、Visual Studio、C\# コードなどの通常の SQL 接続を介して接続することでデータベースを更新できます。

eShopOnContainers アプリケーションは、次のセクションで説明するように、起動時にデータをシードすることにより、各マイクロサービス データベースをサンプル データで初期化します。

SQL Server のコンテナーとしての実行は、SQL Server のインスタンスにアクセスできない場合があるデモに役に立つだけではありません。 説明したように、新しいサンプル データをシードすることによってクリーンな SQL Server イメージと既知のデータから統合テストを簡単に実行できるので開発やテストの環境にも有効です。

#### <a name="additional-resources"></a>その他の技術情報

- **Linux、Mac、Windows で SQL Server Docker イメージを実行する** \
    [https://docs.microsoft.com/sql/linux/sql-server-linux-setup-docker](/sql/linux/sql-server-linux-setup-docker)

- **Linux で sqlcmd を使用して SQL Server に接続してクエリする** \
    [https://docs.microsoft.com/sql/linux/sql-server-linux-connect-and-query-sqlcmd](/sql/linux/sql-server-linux-connect-and-query-sqlcmd)

### <a name="seeding-with-test-data-on-web-application-startup"></a>Web アプリケーションの起動時のテスト データのシード処理

アプリケーションの起動時にデータベースにデータを追加するには、Web API プロジェクトのスタートアップ クラス内の構成メソッドに次のようにコードを追加できます。

```csharp
public class Startup
{
    // Other Startup code...
    public void Configure(IApplicationBuilder app,
        IHostingEnvironment env,
        ILoggerFactory loggerFactory)
    {
        // Other Configure code...
        // Seed data through our custom class
        CatalogContextSeed.SeedAsync(app)
            .Wait();
        // Other Configure code...
    }
}
```

カスタムの CatalogContextSeed クラスの次のコードはデータを入力します。

```csharp
public class CatalogContextSeed
{
    public static async Task SeedAsync(IApplicationBuilder applicationBuilder)
    {
        var context = (CatalogContext)applicationBuilder
            .ApplicationServices.GetService(typeof(CatalogContext));
        using (context)
        {
            context.Database.Migrate();
            if (!context.CatalogBrands.Any())
            {
                context.CatalogBrands.AddRange(
                    GetPreconfiguredCatalogBrands());
                await context.SaveChangesAsync();
            }
            if (!context.CatalogTypes.Any())
            {
                context.CatalogTypes.AddRange(
                    GetPreconfiguredCatalogTypes());
                await context.SaveChangesAsync();
            }
        }
    }

    static IEnumerable<CatalogBrand> GetPreconfiguredCatalogBrands()
    {
        return new List<CatalogBrand>()
       {
           new CatalogBrand() { Brand = "Azure"},
           new CatalogBrand() { Brand = ".NET" },
           new CatalogBrand() { Brand = "Visual Studio" },
           new CatalogBrand() { Brand = "SQL Server" }
       };
    }

    static IEnumerable<CatalogType> GetPreconfiguredCatalogTypes()
    {
        return new List<CatalogType>()
        {
            new CatalogType() { Type = "Mug"},
            new CatalogType() { Type = "T-Shirt" },
            new CatalogType() { Type = "Backpack" },
            new CatalogType() { Type = "USB Memory Stick" }
        };
    }
}
```

統合テストを実行するときには、統合テストと一貫性のあるデータを生成する方法があると便利です。 コンテナーで実行されている SQL Server のインスタンスを含む、すべてのものを新規に作成できると、テスト環境に非常に役立ちます。

### <a name="ef-core-inmemory-database-versus-sql-server-running-as-a-container"></a>EF Core InMemory データベースとコンテナーとして実行される SQL Server

テストの実行時に適した別の選択肢として、Entity Framework InMemory データベース プロバイダーを使用できます。 Web API プロジェクトのスタートアップ クラスの ConfigureServices メソッドでその構成を指定できます。

```csharp
public class Startup
{
    // Other Startup code ...
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddSingleton<IConfiguration>(Configuration);
        // DbContext using an InMemory database provider
        services.AddDbContext<CatalogContext>(opt => opt.UseInMemoryDatabase());
        //(Alternative: DbContext using a SQL Server provider
        //services.AddDbContext<CatalogContext>(c =>
        //{
            // c.UseSqlServer(Configuration["ConnectionString"]);
            //
        //});
    }
  
    // Other Startup code ...
}
```

ただし、重要な落とし穴があります。 メモリ内データベースは、特定のデータベースに固有な多くの制約をサポートしません。 たとえば、EF Core モデルで列に一意のインデックスを追加し、重複する値の追加を許可しないことを確認するためのテストをインメモリ データベースに対して記述する場合があります。 しかし、メモリ内データベースを使用している場合は、列で一意のインデックスを処理することはできません。 そのため、メモリ内データベースは、実際の SQL Server データベースとまったく同じようには動作せず、データベース固有の制約をエミュレートしません。

それでも、テストやプロトタイプ作成にはメモリ内データベースが依然として役立ちます。 特定のデータベースの実装の動作を考慮する正確な統合テストを作成する場合は、SQL Server のような実際のデータベースを使用する必要があります。 その目的のために、コンテナー内での SQL Server の実行は優れた選択肢であり、EF Core InMemory データベース プロバイダーよりも正確です。

### <a name="using-a-redis-cache-service-running-in-a-container"></a>コンテナーで実行されている Redis キャッシュ サービスの使用

特に開発およびテストや概念実証のシナリオで、Redis をコンテナー上で実行できます。 このシナリオは、ローカルの開発用コンピューターだけでなく、CI/CD パイプラインのテスト環境向けにも、コンテナーですべての依存関係を実行できるので便利です。

ただし、実稼働環境で Redis を実行するときは、PaaS (サービスとしてのプラットフォーム) として実行される Redis Microsoft Azure のような高可用性ソリューションを探すことをお勧めします。 コード内で、接続文字列だけを変更する必要があります。

Redis は、Redis と共に Docker イメージを提供します。 そのイメージは、次の URL での Docker Hub から入手できます。

<https://hub.docker.com/_/redis/>

コマンド プロンプトで次の Docker CLI コマンドを実行することによって、Docker Redis コンテナーを直接実行できます。

```console
docker run --name some-redis -d redis
```

Redis イメージには expose:6379 (Redis によって使用されるポート) が含まれているので、標準のコンテナーのリンクを、リンクされたコンテナーが自動的に使用できるようになります。

eShopOnContainers で、basket.api マイクロサービスが、コンテナーとして実行されている Redis キャッシュを使用します。 basket.data コンテナーは、次の例で示すように、マルチコンテナー docker compose.yml ファイルの一部として定義されます。

```yml
#docker-compose.yml file
#...
  basket.data:
    image: redis
    expose:
      - "6379"
```

Docker compose.yml のこのコードは、redis イメージに基づいて basket.data という名前のコンテナーを定義し、ポート 6379 を内部的に公開します。これは、Docker ホスト内で実行されている他のコンテナーからのみアクセスできることを意味します。

最後に、docker compose.override.yml ファイル内の eShopOnContainers サンプルの basket.api マイクロサービスが、その Redis コンテナーに使用する接続文字列を定義します。

```yml
  basket.api:
    environment:
      # Other data ...
      - ConnectionString=basket.data
      - EventBusConnection=rabbitmq
```

前述のように、マイクロサービスの名前 "basket.data" は、docker の内部ネットワーク DNS によって解決されます。

>[!div class="step-by-step"]
>[前へ](multi-container-applications-docker-compose.md)
>[次へ](integration-event-based-microservice-communications.md)
