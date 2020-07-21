---
ms.openlocfilehash: d25c14f93da5fe8acf06269554fed30ddc6bc95d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614756"
---
### <a name="operationcontextcurrent-may-return-null-when-called-in-a-using-clause"></a>OperationContext.Current が using 句で呼びされたときに null を返す場合がある

#### <a name="details"></a>説明

次のすべての条件が満たされている場合は、<xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> が `null` を返し、<xref:System.NullReferenceException> が発生する可能性があります。

- <xref:System.Threading.Tasks.Task> または <xref:System.Threading.Tasks.Task%601> を返すメソッドで <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> プロパティの値を取得します。
- `using` 句で <xref:System.ServiceModel.OperationContextScope> オブジェクトをインスタンス化します。
- `using statement` 内で <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> プロパティの値を取得します。 次に例を示します。

```csharp
using (new OperationContextScope(OperationContext.Current))
{
    // OperationContext.Current is null.
    OperationContext context = OperationContext.Current;

    // ...
}
```

#### <a name="suggestion"></a>提案される解決策

この問題に対処するために、次の操作を行うことができます。

- 次のようにコードを変更して、新しい `null` 以外の <xref:System.ServiceModel.OperationContext.Current%2A> オブジェクトをインスタンス化します。

    ```csharp
    OperationContext ocx = OperationContext.Current;
    using (new OperationContextScope(OperationContext.Current))
    {
        OperationContext.Current = new OperationContext(ocx.Channel);

        // ...
    }
    ```

- 最新の更新プログラムを .NET framework 4.6.2 にインストールするか、最新バージョンの .NET Framework にアップグレードします。 これにより、<xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> で <xref:System.Threading.ExecutionContext> のフローが無効になり、.NET Framework 4.6.1 以前のバージョンで WCF アプリケーションの動作が復元されます。 この動作は構成可能です。構成ファイルに次のアプリ設定を追加することと同じです。

    ```xml
    <appSettings>
      <add key="Switch.System.ServiceModel.DisableOperationContextAsyncFlow" value="true" />
    </appSettings>
    ```

    この変更が望ましくなく、アプリケーションが操作コンテキスト間の実行コンテキスト フローに依存している場合は、次のようにそのフローを有効にできます。

    ```xml
    <appSettings>
      <add key="Switch.System.ServiceModel.DisableOperationContextAsyncFlow" value="false" />
    </appSettings>
    ```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType>
