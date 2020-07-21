---
title: .NET XAML サービスで使用するカスタム型の定義
ms.date: 03/30/2017
helpviewer_keywords:
- defining custom types [XAML Services]
ms.assetid: c2667cbd-2f46-4a7f-9dfc-53696e35e8e4
ms.openlocfilehash: ff7e4229450e801a6d618c5141efde8cdcbef03d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "81433074"
---
# <a name="define-custom-types-for-use-with-net-xaml-services"></a>.NET XAML サービスで使用するカスタム型を定義する

ビジネス オブジェクトであるカスタム型、または特定のフレームワークに依存しない型を定義する場合は、XAML に従うことができる特定のベスト プラクティスがあります。 これらの方法に従うと、.NET XAML サービスとその XAML リーダーおよび XAML ライターは、型の XAML 特性を検出し、XAML 型システムを使用して XAML ノード ストリームで適切な表現を提供できます。 このトピックでは、型定義、メンバー定義、および型またはメンバーの CLR 属性に関するベスト プラクティスについて説明します。

## <a name="constructor-patterns-and-type-definitions-for-xaml"></a>XAML のコンストラクター パターンと型定義

XAML でオブジェクト要素としてインスタンス化するには、カスタム クラスが次の要件を満たしている必要があります。

- カスタム クラスはパブリックである必要があり、パラメーターなしのパブリック コンストラクターを公開する必要があります。 (構造に関する注意事項については、次のセクションを参照してください。

- カスタム クラスは、入れ子になったクラスであってはなりません。 フルネーム パスに追加の "ドット" を指定すると、クラス名前空間の除算があいまいになり、添付プロパティなどの他の XAML 機能と干渉します。
オブジェクトをオブジェクト要素としてインスタンス化できる場合、作成されたオブジェクトは、オブジェクトを基になる型として受け取るプロパティのプロパティ要素フォームに入力できます。

値コンバーターを有効にした場合、これらの基準を満たさない型にオブジェクト値を指定できます。 詳細については、「 [XAML の型コンバーターとマークアップ拡張機能](type-converters-and-markup-extensions.md)」を参照してください。

### <a name="structures"></a>構造体

構造体は、CLR 定義によって常に XAML で構築できます。 これは、CLR コンパイラが構造体のパラメーターなしのコンストラクターを暗黙的に作成するためです。 このコンストラクターは、すべてのプロパティ値を既定値に初期化します。

場合によっては、構造の既定の構築動作が望ましくないことがあります。 これは、構造体が値を埋め、概念的に和集合として機能することを意図している可能性があります。 和集合として、含まれている値は相互に排他的な解釈を持つ可能性があるため、そのプロパティはいずれも設定可能ではありません。 WPF ボキャブラリのこのような構造の例<xref:System.Windows.GridLength>は です。 このような構造体は、構造体値の異なる解釈またはモードを作成する文字列規則を使用して、値を属性形式で表現できるように型コンバーターを実装する必要があります。 構造体は、パラメーターなしのコンストラクターを使用してコード構築の同様の動作を公開する必要もあります。

### <a name="interfaces"></a>インターフェイス

インターフェイスは、基になるメンバーの型として使用できます。 XAML 型システムは、割り当て可能なリストをチェックし、値として提供されるオブジェクトがインターフェイスに割り当てられることを期待します。 関連する割り当て可能な型が XAML 構築要件をサポートしている限り、インターフェイスを XAML 型として表示する方法の概念はありません。

### <a name="factory-methods"></a>工場のメソッド

ファクトリ メソッドは、XAML 2009 の機能です。 オブジェクトにはパラメーターなしのコンストラクターが必要であるという XAML 原則が変更されます。 ファクトリ メソッドについては、この資料では説明しません。 [「x:ファクトリメソッドディレクティブ](xfactorymethod-directive.md)」を参照してください。

## <a name="enumerations"></a>列挙

列挙型には、XAML ネイティブ型の変換動作があります。 XAML で指定された列挙定数名は、基になる列挙型に対して解決され、列挙値を XAML オブジェクト ライターに返します。

XAML では、適用された列挙体に対して<xref:System.FlagsAttribute>フラグ スタイルの使用法がサポートされています。 詳細については[、「XAML 構文の詳細](../../framework/wpf/advanced/xaml-syntax-in-detail.md)」を参照してください。 ([詳細な XAML 構文](../../framework/wpf/advanced/xaml-syntax-in-detail.md)は WPF の対象に記述されていますが、そのトピックの情報のほとんどは、特定の実装フレームワークに固有ではない XAML に関連しています)。

## <a name="member-definitions"></a>メンバー定義

型は、XAML の使用に使用するメンバーを定義できます。 型では、特定の型が XAML で使用できない場合でも、XAML で使用できるメンバーを定義できます。 これは、CLR 継承が原因で可能です。 メンバーを継承する型が XAML の使用法を型としてサポートし、そのメンバーがその基になる型の XAML の使用法をサポートしているか、ネイティブ XAML 構文を使用できる場合、そのメンバーは XAML で使用可能です。

### <a name="properties"></a>Properties

プロパティを、一般的な CLR`get`とアクセサー パターン`set`、および言語に適したキーワードを使用してパブリック CLR プロパティとして定義する場合、XAML 型システムは<xref:System.Xaml.XamlMember>、 および<xref:System.Xaml.XamlMember.IsReadPublic%2A>などの<xref:System.Xaml.XamlMember.IsWritePublic%2A>プロパティに対して提供される適切な情報をメンバとしてプロパティを報告できます。

特定のプロパティを適用することにより、テキスト構文を<xref:System.ComponentModel.TypeConverterAttribute>有効にすることができます。 詳細については、「 [XAML の型コンバーターとマークアップ拡張機能](type-converters-and-markup-extensions.md)」を参照してください。

テキスト構文またはネイティブ XAML 変換が存在しない場合、マークアップ拡張機能の使用など、さらに間接参照がない場合は、(XAML 型システム<xref:System.Xaml.XamlMember.TargetType%2A>内の) プロパティの型は、ターゲット型を CLR 型として扱うことによって、XAML オブジェクト ライターにインスタンスを返すことができる必要があります。

XAML 2009 を使用する場合[、x:参照マークアップ拡張機能](xreference-markup-extension.md)は、前の考慮事項が満たされていない場合に値を提供するために使用できます。ただし、これは型定義の問題よりも使用上の問題です。

### <a name="events"></a>events

イベントをパブリック CLR イベントとして定義すると、XAML 型システムは イベントを メンバー<xref:System.Xaml.XamlMember.IsEvent%2A>として`true`レポートできます。 イベント ハンドラーの配線は、.NET XAML サービス機能の範囲内にありません。配線は、特定のフレームワークと実装に委なされます。

### <a name="methods"></a>メソッド

メソッドのインライン コードは、既定の XAML 機能ではありません。 ほとんどの場合、XAML からメソッド メンバーを直接参照することはなく、XAML のメソッドの役割は、特定の XAML パターンをサポートする目的でのみ行われます。 [x:ファクトリメソッドディレクティブ](xfactorymethod-directive.md)は例外です。

### <a name="fields"></a>フィールド

CLR 設計ガイドラインでは、非静的フィールドを使用しません。 静的フィールドの場合は、 x: Static[マークアップ拡張機能](xstatic-markup-extension.md)を使用して静的フィールド値にアクセスできます。この場合[、x:Static](xstatic-markup-extension.md)の使用用フィールドを公開するために、CLR 定義で特別な操作を行う必要はありません。

## <a name="attachable-members"></a>アタッチ可能なメンバー

アタッチ可能なメンバーは、定義する型のアクセサー メソッド パターンを通じて XAML に公開されます。 定義する型自体は、オブジェクトとして XAML で使用できる必要はありません。 実際には、アタッチ可能なメンバーを所有し、関連する動作を実装する役割を持つサービス クラスを宣言するが、UI 表現などの他の関数を提供しない一般的なパターンです。 次のセクションでは、プレースホルダー *PropertyName*はアタッチ可能なメンバーの名前を表します。 この名前は[XamlName 文法](xamlname-grammar.md)で有効である必要があります。

これらのパターンと型の他のメソッドとの間の名前の衝突には注意してください。 パターンのいずれかに一致するメンバーが存在する場合、意図しなかった場合でも、XAML プロセッサによってアタッチ可能なメンバー使用経路として解釈できます。

#### <a name="the-getpropertyname-accessor"></a>アクセサー

アクセサーのシグネチャ`GetPropertyName`は次の指定が必要です。

`public static object GetPropertyName(object target)`

- `target` オブジェクトは、実装のより具体的な型として指定することができます。 これを使用して、アタッチ可能なメンバーの使用をスコープに設定できます。目的のスコープ外での使用は、無効なキャスト例外をスローし、その後 XAML 解析エラーによって表示されます。 パラメーター名`target`は必須ではありませんが、ほとんどの実装では慣例`target`で名前が付けられています。

- 戻り値は、実装のより具体的な型として指定することができます。

アタッチ可能な<xref:System.ComponentModel.TypeConverter>メンバーの属性の使用に対して有効なテキスト構文を<xref:System.ComponentModel.TypeConverterAttribute>サポートするには`GetPropertyName`、アクセサーに適用します。 の`get`代わりに`set`適用することは直感的ではないようです。ただし、この規則では、シリアル化できる読み取り専用のアタッチ可能なメンバーの概念をサポートできます。

#### <a name="the-setpropertyname-accessor"></a>アクセサー

アクセサーのシグネチャ`SetPropertyName`は次の指定が必要です。

`public static void SetPropertyName(object target, object value)`

- オブジェクト`target`は、前のセクションで説明したように、ロジックと結果を使用して、実装でより具体的な型として指定できます。

- `value` オブジェクトは、実装のより具体的な型として指定することができます。

このメソッドの値は、XAML の使用法からの入力であり、通常は属性形式であることを覚えておいてください。 属性フォームから、テキスト構文の値コンバーターのサポートが必要です`GetPropertyName`。

### <a name="attachable-member-stores"></a>アタッチ可能なメンバ ストア

通常、アクセサー メソッドでは、アタッチ可能なメンバー値をオブジェクト グラフに配置したり、オブジェクト グラフから値を取得して適切にシリアル化したりする手段を提供するには十分ではありません。 この機能を提供するには、`target`前のアクセサー シグネチャのオブジェクトが値を格納できる必要があります。 ストレージ・メカニズムは、アタッチ可能メンバーがメンバー・リストにないターゲットにメンバーをアタッチできる、というアタッチ可能メンバーの原則と一致している必要があります。 .NET XAML サービスは、API<xref:System.Xaml.IAttachedPropertyStore>と を介してアタッチ可能な<xref:System.Xaml.AttachablePropertyServices>メンバ ストアの実装手法を提供します。 <xref:System.Xaml.IAttachedPropertyStore>は、XAML ライターがストアの実装を検出するために使用し、アクセサー`target`の型に実装する必要があります。 静的<xref:System.Xaml.AttachablePropertyServices>API はアクセサーの本体内で使用され、そのアクセサーによってアタッチ可能なメンバーを<xref:System.Xaml.AttachableMemberIdentifier>参照します。

## <a name="xaml-related-clr-attributes"></a>XAML 関連の CLR 属性

型、メンバー、およびアセンブリに正しく関連付けられているのは、XAML 型システム情報を .NET XAML サービスに報告するために重要です。 次のいずれかの状況に該当する場合は、XAML 型システム情報のレポートが関連します。

- 型は、.NET XAML サービス XAML リーダーと XAML ライターに直接基づく XAML システムで使用する予定です。
- これらの XAML リーダーと XAML ライターに基づく XAML を使用するフレームワークを定義または使用します。

カスタム型の XAML サポートに関連する各 XAML 関連の属性の一覧については、「[カスタム型とライブラリの XAML 関連](clr-attributes-with-custom-types-and-libraries.md)CLR 属性」を参照してください。

## <a name="usage"></a>使用法

カスタム型を使用するには、マークアップ作成者が、カスタム型を含むアセンブリと CLR 名前空間のプレフィックスをマップする必要があります。 この手順については、このトピックでは説明しません。

## <a name="access-level"></a>アクセス レベル

XAML は、アクセス レベルを持つ型を`internal`読み込んでインスタンス化する手段を提供します。 この機能は、ユーザー コードが独自の型を定義し、同じユーザー コード スコープの一部でもあるマークアップからそれらのクラスをインスタンス化できるように提供されています。

WPF の例は、ユーザー コードが<xref:System.Windows.Controls.UserControl>UI 動作をリファクタリングする方法として定義されているが、アクセス レベルで`public`サポート クラスを宣言することによって暗黙の拡張メカニズムの一部としては定義されない場合です。 このような<xref:System.Windows.Controls.UserControl>a は、XAML 型として`internal`参照されるアセンブリと同じアセンブリにバッキング コードがコンパイルされている場合に、access を使用して宣言できます。

完全信頼の下で XAML を読み<xref:System.Xaml.XamlObjectWriter>込み、`internal`を使用するアプリケーションでは、アクセス レベルを持つクラスの読み込みは常に有効になります。

部分信頼の下で XAML を読み込むアプリケーションの場合は、API<xref:System.Xaml.Permissions.XamlAccessLevel>を使用してアクセス レベルの特性を制御できます。 また、遅延メカニズム (WPF テンプレート システムなど) は、アクセス レベルのアクセス許可を伝達し、最終的な実行時評価のためにそれらを保持できる必要があります。これは、情報を渡すことによって内部的に<xref:System.Xaml.Permissions.XamlAccessLevel>処理されます。

### <a name="wpf-implementation"></a>WPF の実装

WPF XAML は、部分的な信頼の下で BAML が読み込まれる場合、BAML ソースであるアセンブリに対する<xref:System.Xaml.Permissions.XamlAccessLevel.AssemblyAccessTo%2A>アクセスが制限される部分信頼アクセス モデルを使用します。 遅延の場合、WPF<xref:System.Xaml.IXamlObjectWriterFactory.GetParentSettings%2A?displayProperty=nameWithType>はアクセス レベル情報を渡すためのメカニズムとして使用します。

WPF XAML 用語では、*内部型*は、参照元の XAML も含む同じアセンブリによって定義される型です。 このような型は、マップの assembly= 部分を意図的に省略する XAML 名前空間を通じてマップできます`xmlns:local="clr-namespace:WPFApplication1"`。 BAML が内部型を参照し、その`internal`型にアクセス レベルがある場合`GeneratedInternalTypeHelper`、アセンブリのクラスが生成されます。 を避`GeneratedInternalTypeHelper`ける場合は、アクセス レベルを`public`使用するか、関連するクラスを別のアセンブリに分類してそのアセンブリを依存させる必要があります。

## <a name="see-also"></a>関連項目

- [カスタム型およびライブラリの XAML 関連の CLR 属性](clr-attributes-with-custom-types-and-libraries.md)
- [XAML サービス](../../../api/index.md)
