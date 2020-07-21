---
title: C# の予約済み属性:Conditional、Obsolete、AttributeUsage
ms.date: 04/09/2020
description: これらの属性はコンパイラによって解釈され、コンパイラによって生成されたコードに影響を与えます
ms.openlocfilehash: c6d697dd08233ffc88900949998047137ee170a9
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021769"
---
# <a name="reserved-attributes-conditionalattribute-obsoleteattribute-attributeusageattribute"></a>予約済みの属性:ConditionalAttribute、ObsoleteAttribute、AttributeUsageAttribute

これらの属性は、コード内の要素に適用できます。 それによって、このような要素にセマンティックの意味が追加されます。 コンパイラでは、これらのセマンティックの意味を使用して出力が変更され、コードを使用する開発者による間違いの可能性が報告されます。

## <a name="conditional-attribute"></a>`Conditional` 属性

`Conditional` 属性を使用すると、プリプロセス識別子に依存したメソッドの実行を指定できます。 `Conditional` 属性は <xref:System.Diagnostics.ConditionalAttribute> の別名であり、メソッドまたは属性クラスに適用できます。

次の例では、`Conditional` は、プログラム固有の診断情報の表示を有効または無効にするメソッドに適用されています。

:::code language="csharp" source="snippets/trace.cs" interactive="try-dotnet" :::

`TRACE_ON` 識別子が定義されていない場合、トレース出力は表示されません。 対話型ウィンドウで自分で探してください。

多くの場合、`Conditional` 属性は、リリース ビルドではなく、デバッグ ビルドのトレース機能とログ機能を有効にするために `DEBUG` 識別子と共に使用されます。次に例を示します。

:::code language="csharp" source="snippets/ConditionalExamples.cs" id="SnippetConditional" :::

条件付きの印が付いたメソッドが呼び出されると、指定のプリプロセッサ シンボルの有無に従って、呼び出しの実行か省略が決定されます。 シンボルが定義されている場合は呼び出しが実行され、定義されていない場合は省略されます。 条件付きメソッドは、クラスまたは構造体宣言のメソッドである必要があり、戻り値の型が `void` である必要があります。 `Conditional` を使用すると、`#if…#endif` ブロック内にメソッドを含めるよりも、クリーンで洗練されており、エラーが発生しにくくなります。

メソッドに複数の `Conditional` 属性が付いている場合、そのメソッドの呼び出しは、1 つ以上の条件付きシンボルが定義されているときに実行されます (シンボルは OR 演算子によって論理的にリンクされています)。 次の例では、`A` または `B` が存在すると、メソッドが呼び出されます。

:::code language="csharp" source="snippets/ConditionalExamples.cs" id="SnippetMultipleConditions" :::

### <a name="using-conditional-with-attribute-classes"></a>属性クラスでの `Conditional` の使用

`Conditional` 属性は、属性クラスの定義にも適用できます。 次の例では、カスタム属性 `Documentation` は、`DEBUG` が定義されている場合にのみ、情報をメタデータに追加します。

:::code language="csharp" source="snippets/ConditionalExamples.cs" id="SnippetConditionalConditionalAttribute" :::

## <a name="obsolete-attribute"></a>`Obsolete` 属性

`Obsolete` 属性は、コード要素の使用が推奨されなくなったことを示します。 非推奨とマークされたエンティティを使用すると、警告またはエラーが生成されます。 `Obsolete` 属性は、1 回だけ使用できる属性であり、属性を使用できる任意のエンティティに適用できます。 `Obsolete` は <xref:System.ObsoleteAttribute> の別名です。

次の例では、`Obsolete` 属性がクラス `A` およびメソッド `B.OldMethod` に適用されています。 `B.OldMethod` に適用された属性コンストラクターの 2 番目の引数が `true` に設定されているため、このメソッドではコンパイル エラーが発生します。一方、クラス `A` が使用されると、警告が生成されます。 しかし、`B.NewMethod` の呼び出しでは、警告もエラーも生成されません。 たとえば、前の定義でこれを使用すると、次のコードで 2 つの警告と 1 つのエラーが生成されます。

:::code language="csharp" source="snippets/ObsoleteExample.cs" interactive="try-dotnet" :::

最初の引数として属性コンストラクターに指定された文字列は、警告またはエラーの一部として表示されます。 クラス `A` の警告が 2 つ生成されます。1 つはクラス参照の宣言の警告で、もう 1 つはクラス コンストラクターの警告です。 `Obsolete` 属性は引数なしで使用できますが、代わりに何を使用するかの説明を含めることをお勧めします。

## <a name="attributeusage-attribute"></a>`AttributeUsage` 属性

`AttributeUsage` 属性によって、カスタム属性クラスの使用方法が決まります。 <xref:System.AttributeUsageAttribute> は、カスタム属性定義に適用する属性です。 `AttributeUsage` 属性を使用すると、以下を制御できます。

- 適用できるプログラム要素属性。 使用法を制限しない限り、属性は以下のプログラム要素のいずれかに適用できます。
  - アセンブリ
  - name
  - フィールド
  - event
  - メソッド
  - param
  - property
  - return
  - 型
- 1 つのプログラム要素に属性を複数回適用できるかどうか。
- 属性が派生クラスに継承されるかどうか。

明示的に適用すると、既定の設定は次の例のようになります。

:::code language="csharp" source="snippets/NewAttribute.cs" id="SnippetUsageFirst" :::

この例で `NewAttribute` クラスはサポートされている任意のプログラム要素に適用できます。 ただし、各エンティティに適用できるのは 1 回のみです。 基底クラスに適用すると、属性は派生クラスに継承されます。

<xref:System.AttributeUsageAttribute.AllowMultiple> 引数と <xref:System.AttributeUsageAttribute.Inherited> 引数は省略できるので、次のコードは同じ効果を持ちます。

:::code language="csharp" source="snippets/NewAttribute.cs" id="SnippetUsageSecond" :::

最初の <xref:System.AttributeUsageAttribute> 引数は、<xref:System.AttributeTargets> 列挙型の 1 つまたは複数の要素でなければなりません。 次の例のように、複数のターゲット型を OR 演算子で 1 つにまとめることができます。

:::code language="csharp" source="snippets/NewPropertyOrFieldAttribute.cs" id="SnippetDefinePropertyAttribute" :::

C# 7.3 以降、プロパティ、または自動実装バッキング フィールドに属性を適用できるようになりました。 属性に `field` 指定子を指定しない限り、属性はプロパティに適用されます。 その両方の例を次に示します。

:::code language="csharp" source="snippets/NewPropertyOrFieldAttribute.cs" id="SnippetUsePropertyAttribute" :::

<xref:System.AttributeUsageAttribute.AllowMultiple> 引数が `true` の場合、次の例のように、結果の属性を 1 つのエンティティに複数回適用できます。

:::code language="csharp" source="snippets/MultiUseAttribute.cs" id="SnippetMultiUse" :::

この例では、`AllowMultiple` が `true` に設定されているので、`MultiUseAttribute` を繰り返し適用できます。 示されているどちらの形式でも、複数の属性を適用できます。

<xref:System.AttributeUsageAttribute.Inherited> が `false` の場合、属性は属性クラスから派生したクラスに継承されません。 次に例を示します。

:::code language="csharp" source="snippets/NonInheritedAttribute.cs" id="SnippetNonInherited" :::

この例で、`NonInheritedAttribute` は継承によって `DClass` に適用されません。

## <a name="see-also"></a>関連項目

- <xref:System.Attribute>
- <xref:System.Reflection>
- [属性](../../../standard/attributes/index.md)
- [リフレクション](../../programming-guide/concepts/reflection.md)
