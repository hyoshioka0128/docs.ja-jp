---
ms.openlocfilehash: 35fc4782ebbba33f5fc6668712af9d89d00cafe9
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614975"
---
### <a name="wpf-changing-a-primary-key-when-displaying-ado-data-in-a-masterdetail-scenario"></a>WPF のマスター/詳細シナリオで ADO データを表示するときに主キーが変更される

#### <a name="details"></a>説明

`Order` 型の項目の ADO コレクションと、それを主キー &quot;OrderID&quot; によって `Detail` 型の項目のコレクションに関連付ける &quot;OrderDetails&quot; という関係があるとします。 WPF アプリでは、特定の順序の詳細にリスト コントロールをバインドできます。

```xaml
<ListBox ItemsSource="{Binding Path=OrderDetails}" >
```

ここで、DataContext は `Order` です。 WPF により、`OrderDetails` プロパティの値 (`OrderID` がマスター項目の `OrderID` と一致するすべての `Detail` 項目のコレクション D) が取得されます。 マスター項目の主キー `OrderID` を変更すると、動作の変更が発生します。 ADO は、Details コレクション内の影響を受ける各レコード (つまり、コレクション D にコピーされたレコード) の `OrderID` を自動的に変更します。  では、D はどうなるのでしょうか?

- 以前の動作:コレクション D はクリアされます。 マスター項目では、プロパティ  *の変更通知が*発生しません`OrderDetails`。 ListBox は、空になったコレクション D を引き続き使用します。
- 新しい動作:コレクション D は変更されません。 その各項目で、`OrderID` プロパティの変更通知が発生します。 ListBox はコレクション D を引き続き使用し、新しい `OrderID` に関する詳細を表示します。 WPF は、別の方法 (`followParent` 引数を `true` に設定して ADO メソッド <xref:System.Data.DataRowView.CreateChildView(System.Data.DataRelation,System.Boolean)?displayProperty=nameWithType> を呼び出す) でコレクション D を作成することにより、新しい動作を実装します。

#### <a name="suggestion"></a>提案される解決策

アプリは、次の AppContext スイッチを使用して新しい動作を取得します。

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Data.DoNotUseFollowParentWhenBindingToADODataRelation=false"/>
  </runtime>
</configuration>
```

スイッチの既定値は、.NET 4.7.1 以下を対象とするアプリでは `true` に設定され (古い動作)、.NET 4.7.2 以上を対象とするアプリでは `false` に設定されます (新しい動作)。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
