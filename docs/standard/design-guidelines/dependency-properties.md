---
title: 依存関係プロパティ
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 212cfb1e-cec4-4047-94a6-47209b387f6f
ms.openlocfilehash: 476ef1bb1ac5ec1f551979c64a41cbae55c554bc
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280258"
---
# <a name="dependency-properties"></a>依存関係プロパティ
依存関係プロパティ (DP) は、など、型の変数 (field) に格納するのではなく、プロパティストアにその値を格納する通常のプロパティです。

 アタッチされる依存関係プロパティは、静的な Get および Set メソッドとしてモデル化された依存関係プロパティの一種で、オブジェクトとそのコンテナーの間のリレーションシップ (コンテナー上のオブジェクトの位置など) を表す "プロパティ" を表し `Button` `Panel` ます。

 スタイル設定、トリガー、データバインディング、アニメーション、動的リソース、継承などの WPF 機能をサポートするためにプロパティが必要な場合は、依存関係プロパティを指定✔️ます。

## <a name="dependency-property-design"></a>依存関係プロパティのデザイン
 <xref:System.Windows.DependencyObject>依存関係プロパティを実装するときに、✔️、またはそのサブタイプの1つを継承します。 型は、プロパティストアの非常に効率的な実装を提供し、WPF のデータバインディングを自動的にサポートします。

 ✔️は、 <xref:System.Windows.DependencyProperty?displayProperty=nameWithType> 依存関係プロパティごとにのインスタンスを格納する通常の CLR プロパティとパブリックの静的読み取り専用フィールドを提供します。

 インスタンスメソッドとを呼び出すことによって、依存関係プロパティを実装✔️ <xref:System.Windows.DependencyObject.GetValue%2A?displayProperty=nameWithType> <xref:System.Windows.DependencyObject.SetValue%2A?displayProperty=nameWithType> ます。

 ✔️プロパティの名前を "suffixing" にして、依存関係プロパティの静的フィールドに名前を付けます。

 ❌コードで依存関係プロパティの既定値を明示的に設定しないでください。代わりに、メタデータに設定します。

 プロパティの既定値を明示的に設定した場合、スタイル設定などのいくつかの暗黙的な方法によってそのプロパティが設定されないようにすることができます。

 ❌静的フィールドにアクセスするために、標準コード以外のプロパティアクセサーにコードを配置しないでください。

 スタイル設定などの暗黙的な方法によってプロパティが設定されている場合、そのコードは実行されません。これは、スタイルが静的フィールドを直接使用するためです。

 ❌セキュリティで保護されたデータを格納するために依存関係プロパティを使用しないでください。 プライベート依存関係プロパティも、パブリックにアクセスできます。

## <a name="attached-dependency-property-design"></a>アタッチされた依存関係プロパティのデザイン
 前のセクションで説明した依存関係プロパティは、宣言する型の組み込みプロパティを表します。たとえば、プロパティは、を `Text` 宣言するのプロパティです `TextButton` 。 特別な種類の依存関係プロパティは、アタッチされる依存関係プロパティです。

 添付プロパティの従来の例として、 <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> プロパティがあります。 プロパティは、ボタンの (グリッドではなく) 列の位置を表しますが、グリッドにボタンが含まれている場合にのみ関連し、グリッドによってボタンに "アタッチ" されます。

```xaml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>

    <Button Grid.Column="0">Click</Button>
    <Button Grid.Column="1">Clack</Button>
</Grid>
```

 添付プロパティの定義は、通常の依存関係プロパティとほとんど同じように見えますが、アクセサーは静的な Get メソッドと Set メソッドによって表される点が異なります。

```csharp
public class Grid {

    public static int GetColumn(DependencyObject obj) {
        return (int)obj.GetValue(ColumnProperty);
    }

    public static void SetColumn(DependencyObject obj, int value) {
        obj.SetValue(ColumnProperty,value);
    }

    public static readonly DependencyProperty ColumnProperty =
        DependencyProperty.RegisterAttached(
            "Column",
            typeof(int),
            typeof(Grid)
    );
}
```

## <a name="dependency-property-validation"></a>依存関係プロパティの検証
 プロパティは、多くの場合、検証と呼ばれるものを実装します。 検証ロジックは、プロパティの値を変更しようとしたときに実行されます。

 残念ながら、依存関係プロパティのアクセサーに任意の検証コードを含めることはできません。 代わりに、プロパティの登録時に依存関係プロパティの検証ロジックを指定する必要があります。

 ❌プロパティのアクセサーに依存関係プロパティの検証ロジックを配置しないでください。 代わりに、検証コールバックをメソッドに渡し `DependencyProperty.Register` ます。

## <a name="dependency-property-change-notifications"></a>依存関係プロパティの変更通知
 ❌依存関係プロパティのアクセサーには、変更通知ロジックを実装しないでください。 依存関係プロパティには、に変更通知コールバックを提供することによって使用する必要がある、組み込みの変更通知機能があり <xref:System.Windows.PropertyMetadata> ます。

## <a name="dependency-property-value-coercion"></a>依存関係プロパティ値の強制変換
 プロパティの強制変換は、プロパティの set アクセス操作子に渡された値が setter によって変更されたときに、プロパティストアが実際に変更される前に行われます。

 ❌依存関係プロパティアクセサーに強制型変換ロジックを実装しないでください。

 依存関係プロパティには組み込みの強制型変換機能があり、への強制変換コールバックを提供することによって使用でき `PropertyMetadata` ます。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [一般的なデザインパターン](common-design-patterns.md)
