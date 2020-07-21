---
title: x:Static のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- StaticExtension
- xStatic
- x:Static
helpviewer_keywords:
- x:Static markup extension [XAML Services]
- Static markup extension in XAML [XAML Services]
- XAML [XAML Services], x:Static markup extension
ms.assetid: 056aee79-7cdd-434f-8174-dfc856cad343
ms.openlocfilehash: fb9ee6807135f17fd9e0c799533bba28b369ebe2
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "81433266"
---
# <a name="xstatic-markup-extension"></a>x:Static のマークアップ拡張機能

共通言語仕様 (CLS) に準拠した方法で定義されている静的な値によるコード エンティティを参照します。 参照される静的プロパティを使用して、XAML でプロパティの値を提供できます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object property="{x:Static prefix:typeName.staticMemberName}" .../>
```

## <a name="xaml-values"></a>XAML 値

| | |
|-|-|
|`prefix`|省略可能。 マップされた既定以外の XAML 名前空間を参照するプレフィックス。 `prefix`は、既定の XAML 名前空間から取得した静的プロパティを参照することはほとんどありませんので、使用法で明示的に示されています。 「解説」を参照してください。|
|`typeName`|必須。 目的の静的メンバーを定義する型の名前。|
|`staticMemberName`|必須。 目的の静的値メンバー (定数、静的プロパティ、フィールド、または列挙値) の名前。|

## <a name="remarks"></a>解説

参照されるコード エンティティは、次のいずれかである必要があります。

- 定数
- 静的プロパティ
- フィールド
- 列挙値

非静的プロパティなどの他のコード エンティティを指定すると、XAML がマークアップ コンパイルされた場合にコンパイル エラーが発生したり、XAML の読み込み時解析例外が発生します。

現在の`x:Static`XAML ドキュメントの既定の XAML 名前空間にない静的フィールドまたはプロパティへの参照を作成できます。ただし、この場合はプレフィックスマッピングが必要です。 XAML 名前空間は、ほとんどの場合、XAML ドキュメントのルート要素で定義されます。

静的プロパティの検索操作は、.NET XAML サービス、XAML リーダー、および XAML ライターが既定の XAML スキーマ コンテキストで実行しているときに実行できます。 この XAML スキーマ コンテキストでは、CLR リフレクションを使用して、オブジェクト グラフの構築に必要な静的な値を提供できます。 指定`typeName`するのは、実際には CLR 型名ではなく、XAML 型名ですが、既定の XAML スキーマ コンテキストを使用する場合や、既存のすべての CLR ベースの XAML 実装フレームワークを使用する場合は、基本的に同じ名前です。

プロパティの値の型`x:Static`を直接参照しない場合は注意が必要です。 XAML 処理シーケンスでは、マークアップ拡張機能から提供された値は、追加の値変換を呼び出しません。 これは、参照でテキスト文字列`x:Static`が作成され、テキスト文字列に基づく属性値の値の変換が通常、その特定のメンバーまたは戻り値の型のメンバー値に対して行われる場合でも当てはまります。

属性構文は、このマークアップ拡張機能で使用される最も一般的な構文です。 `x:Static` 識別子文字列の後に設定される文字列トークンは、基になる <xref:System.Windows.Markup.StaticExtension.Member%2A> 拡張クラスの <xref:System.Windows.Markup.StaticExtension> 値として割り当てられます。

技術的に可能な XAML の使用方法は他に 2 つあります。 ただし、これらの使用法は不必要に冗長であるため、あまり一般的ではありません。

01. オブジェクト要素の構文。

    ```xaml
    <x:Static Member="prefix:typeName.staticMemberName" ... />
    ```

02. 初期化文字列に明示的な Member プロパティを持つ属性構文。

    ```xaml
    <object property="{x:Static Member=prefix:typeName.staticMemberName}" ... />
    ```

NET XAML サービスの実装では、このマークアップ拡張機能の処理は、クラスによって<xref:System.Windows.Markup.StaticExtension>定義されます。

`x:Static` はマークアップ拡張機能です。 XAML のすべてのマークアップ拡張機能は、`{`属性`}`構文で、 および 文字を使用します。 マークアップ拡張機能について詳しくは、「 [Markup Extensions for XAML Overview](markup-extensions-overview.md)」をご覧ください。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

WPF プログラミングに使用する既定の XAML 名前空間には、便利な静的プロパティが多く含まれていないため、便利な静的プロパティのほとんどでは、使用を容易にする型`{x:Static}`コンバーターなどのサポートがあります。 静的プロパティの場合、次のいずれかに該当する場合は、XAML 名前空間のプレフィックスをマップする必要があります。

- WPF に存在するが、WPF ( )`http://schemas.microsoft.com/winfx/2006/xaml/presentation`の既定の XAML 名前空間の一部ではない型を参照しています。 これは、 を使用`x:Static`する場合にはかなり一般的なシナリオです。 たとえば、`x:Static`<xref:System>クラスの静的プロパティを参照するために、CLR 名前空間と mscorlib アセンブリに対する XAML 名前空間マッピングを持つ<xref:System.Environment>参照を使用できます。

- カスタム アセンブリから型を参照しています。

- WPF アセンブリ内に存在する型を参照していますが、その型は、WPF の既定の XAML 名前空間の一部としてマップされていない CLR 名前空間内にあります。 CLR 名前空間の既定の XAML 名前空間へのマッピングは、さまざまな WPF アセンブリの定義によって実行されます (この概念の詳細については[、「XAML 名前空間と WPF XAML の名前空間マッピング](../../framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)」を参照してください)。 マップされていない CLR 名前空間は、CLR 名前空間が XAML 用ではないクラス定義の大部分で構成されている場合に存在する可能性があります<xref:System.Windows.Threading>。

WPF のプレフィックスと XAML 名前空間を使用する方法の詳細については、「 WPF XAML の[XAML 名前空間と名前空間マッピング](../../framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [x:Type マークアップ拡張機能](xtype-markup-extension.md)
- [WPF から System.Xaml に移行した型](../../framework/wpf/advanced/types-migrated-from-wpf-to-system.md)
