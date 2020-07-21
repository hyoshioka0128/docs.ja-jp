---
title: Windows フォームデザイナーのデザイン時エラー
titleSuffix: ''
description: コード、サードパーティコンポーネント、または他の場所でエラーが発生したために Windows フォームデザイナーの読み込みに失敗した場合に発生するエラーについて説明します。
ms.date: 09/09/2019
f1_keywords:
- DTELErrorList
- WhyDTELPage
helpviewer_keywords:
- errors [Windows Forms Designer]
- design-time errors [Windows Forms Designer]
ms.assetid: ad408380-825a-46d8-9a4a-531b130b88ce
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d9c3993dfce9312c3271c499b6c0cd0c11253ca8
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904391"
---
# <a name="windows-forms-designer-error-page"></a>Windows フォームデザイナーのエラーページ

コードのエラー、サードパーティのコンポーネント、または他の場所でエラーが発生したために Windows フォームデザイナーの読み込みに失敗した場合は、デザイナーではなくエラーページが表示されます。 このエラーページは、必ずしもデザイナーのバグを示しているわけではありません。 バグは、という名前の分離コードページのどこかにある可能性があり \<your-form-name> ます。Designer.cs。 エラーは、コードページのエラーの場所に移動するためのリンクを含む、折りたたみ可能な黄色のバーに表示されます。

![Windows フォームデザイナーのエラーページ](media/windows-forms-designer-error-page-collapsed.png)

エラーを無視してデザイナーの読み込みを続行するには、[**無視して続行**] をクリックします。 この操作によって予期しない動作が発生する可能性があります。たとえば、コントロールがデザインサーフェイスに表示されないことがあります。

## <a name="instances-of-this-error"></a>このエラーのインスタンス

黄色のエラーバーが展開されると、エラーの各インスタンスが一覧表示されます。 多くのエラーの種類には、 *[プロジェクト名]* *[フォーム名]* 行:*[行番号]* 列:*[列番号]* の形式の正確な場所が含まれています。 コールスタックがエラーに関連付けられている場合は、[**呼び出し履歴の表示**] リンクをクリックすると、呼び出し履歴が表示されます。 呼び出し履歴を調べると、エラーの解決に役立つ場合があります。

![Windows フォームデザイナー展開されたエラー](media/windows-forms-designer-error-page-expanded.png)

> [!NOTE]
>
> - Visual Basic アプリの場合、[デザイン時エラー] ページには複数のエラーが表示されませんが、同じエラーの複数のインスタンスが表示されることがあります。
> - C++ アプリの場合、エラーにはコードの場所のリンクがありません。

## <a name="help-with-this-error"></a>このエラーに関するヘルプ

エラーのヘルプトピックが表示されている場合は、 **MSDN のヘルプ**リンクをクリックして、docs.microsoft.com のヘルプページに直接移動します。

## <a name="forum-posts-about-this-error"></a>このエラーに関するフォーラムの投稿

[**このエラーに関連する投稿を MSDN フォーラムで検索**する] リンクをクリックして、Microsoft Developer Network フォーラムに移動します。 [Windows フォームデザイナー](https://social.msdn.microsoft.com/Forums/windows/home?forum=winformsdesigner)または[Windows フォーム](https://social.msdn.microsoft.com/Forums/windows/home?category=windowsforms)フォーラムを具体的に検索することもできます。

## <a name="design-time-errors"></a>デザイン時エラー

ここでは、発生する可能性のあるエラーの一部を示します。

### <a name="identifier-name-is-not-a-valid-identifier"></a>' \<identifier name> ' は有効な識別子ではありません。

このエラーは、フィールド、メソッド、イベント、またはオブジェクトの名前が不適切であることを示します。

### <a name="name-already-exists-in-project-name"></a>' ' \<name> は既に ' ' に存在します。 \<project name>

エラーメッセージ: "' ' \<name> は既に ' ' に存在し \<project name> ます。 一意の名前を入力してください。 "

プロジェクトに既に存在する継承されたフォームの名前を指定しました。 このエラーを修正するには、継承されたフォームに一意の名前を付けます。

### <a name="toolbox-tab-name-is-not-a-toolbox-category"></a>' \<Toolbox tab name> ' はツールボックスカテゴリではありません。

サードパーティのデザイナーが、存在しないツールボックスのタブにアクセスしようとしました。 コンポーネントのベンダにお問い合わせください。

### <a name="a-requested-language-parser-is-not-installed"></a>要求された言語パーサーはインストールされていません。

エラーメッセージ: "要求された言語パーサーがインストールされていません。 言語パーサー名は ' {0} ' です。 "

Visual Studio によって、ファイルの種類に登録されているデザイナーの読み込みが試行されましたが、読み込めませんでした。 これは、セットアップ中に発生したエラーが原因である可能性があります。 修正のために使用している言語のベンダにお問い合わせください。

### <a name="a-service-required-for-generating-and-parsing-source-code-is-missing"></a>ソース コードの生成、解析に必要なサービスがありません。

これは、サードパーティのコンポーネントに問題があります。 コンポーネントのベンダにお問い合わせください。

### <a name="an-exception-occurred-while-trying-to-create-an-instance-of-object-name"></a>' ' のインスタンスを作成しようとしているときに例外が発生しました。 \<object name>

エラーメッセージ: "' ' のインスタンスを作成しようとして例外が発生しました \<object name> 。 例外は "" でした \<exception string\> 。

サードパーティのデザイナーによって、Visual Studio がオブジェクトを作成するように要求しましたが、オブジェクトでエラーが発生しました。 コンポーネントのベンダにお問い合わせください。

### <a name="another-editor-has-document-name-open-in-an-incompatible-mode"></a>別のエディターで ' ' が互換性のない \<document name> モードで開かれています。

エラーメッセージ: "別のエディターで ' ' が互換性のない \<document name> モードで開かれています。 エディターを閉じて、この操作をもう一度お試しください。 "

このエラーは、別のエディターで既に開かれているファイルを開こうとした場合に発生します。 ファイルが既に開いているエディターが表示されます。 このエラーを修正するには、ファイルが開いているエディターを閉じて、もう一度やり直してください。

### <a name="another-editor-has-made-changes-to-document-name"></a>別のエディターによって ' ' が変更されました。 \<document name>

変更を有効にするには、デザイナーを閉じてから開き直します。 通常、変更が加えられると、Visual Studio によってデザイナーが自動的に再読み込みされます。 ただし、サードパーティのコンポーネントデザイナーなど、他のデザイナーでは、再読み込み動作がサポートされていない場合があります。 この場合、Visual Studio では、デザイナーを閉じて再度開くように求められます。

### <a name="another-editor-has-the-file-open-in-an-incompatible-mode"></a>別のエディターによって互換性のないモードでファイルが開かれています。

エラーメッセージ: "別のエディターで、互換性のないモードでファイルが開かれています。 エディターを閉じて、この操作をもう一度お試しください。 "

このメッセージは、"別のエディターが互換性のない \<document name> モードで開いています" と似ていますが、Visual Studio はファイル名を特定できません。 このエラーを修正するには、ファイルが開いているエディターを閉じて、もう一度やり直してください。

### <a name="array-rank-rank-in-array-is-too-high"></a>配列ランク ' \<rank in array> ' が大きすぎます

Visual Studio では、デザイナーによって解析されるコードブロック内の1次元配列のみがサポートされます。 多次元配列は、この領域の外側で有効です。

### <a name="assembly-assembly-name-could-not-be-opened"></a>アセンブリ ' \<assembly name> ' を開けませんでした

エラーメッセージ: "アセンブリ ' \<assembly name> ' を開けませんでした。 ファイルがまだ存在していることを確認してください。 "

このエラーメッセージは、開くことができなかったファイルを開こうとしたときに発生します。 ファイルが存在し、有効なアセンブリであることを確認してください。

### <a name="bad-element-type-this-serializer-expects-an-element-of-type-type-name"></a>要素の型が正しくありません。 このシリアライザーには ' ' 型の要素が必要です \<type name>

これは、サードパーティのコンポーネントに問題があります。 コンポーネントのベンダにお問い合わせください。

### <a name="cannot-access-the-visual-studio-toolbox-at-this-time"></a>現在 Visual Studio の Toolbox にアクセスできません。

Visual Studio によってツールボックスが呼び出されましたが、これは使用できませんでした。 このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="cannot-bind-an-event-handler-to-the-event-name-event-because-it-is-read-only"></a>イベントハンドラーは読み取り専用なので、イベントハンドラーを ' ' イベントにバインドできません。 \<event name>

このエラーは、基本クラスから継承されたコントロールにイベントを接続しようとした場合によく発生します。 コントロールのメンバー変数がプライベートである場合、Visual Studio はイベントをメソッドに接続できません。 プライベートに継承されたコントロールには、追加のイベントをバインドすることはできません。

### <a name="cannot-create-a-method-name-for-the-requested-component-because-it-is-not-a-member-of-the-design-container"></a>デザイン コンテナーのメンバーでないため、要求されたコンポーネントのメソッド名を作成できません。

Visual Studio が、デザイナーにメンバー変数を持たないコンポーネントにイベントハンドラーを追加しようとしました。 コンポーネントのベンダにお問い合わせください。

### <a name="cannot-name-the-object-name-because-it-is-already-named-name"></a>オブジェクト ' ' には \<name> 既に ' ' という名前が付けられているため、名前を指定できません。 \<name>

これは、Visual Studio シリアライザーでの内部エラーです。 これは、シリアライザーがオブジェクトに2回名前を指定しようとしたことを示します。これはサポートされていません。 このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="cannot-remove-or-destroy-inherited-component-component-name"></a>継承されたコンポーネント ' ' を削除または破棄できません。 \<component name>

継承されたコントロールは、継承するクラスの所有権を持ちます。 継承されたコントロールに対する変更は、コントロールの生成元のクラスで行う必要があります。 そのため、名前を変更したり、破棄したりすることはできません。

### <a name="category-toolbox-tab-name-does-not-have-a-tool-for-class-class-name"></a>カテゴリ ' \<Toolbox tab name> ' には、クラス ' ' のツールがありません。 \<class name>

デザイナーが特定の [ツールボックス] タブのクラスを参照しようとしましたが、このクラスは存在しません。 コンポーネントのベンダにお問い合わせください。

### <a name="class-class-name-has-no-matching-constructor"></a>クラス ' \<class name> ' には一致するコンストラクターがありません。

サードパーティのデザイナーが Visual Studio に対して、存在しないコンストラクターに特定のパラメーターを持つオブジェクトを作成するように要求しました。 コンポーネントのベンダにお問い合わせください。

### <a name="code-generation-for-property-property-name-failed"></a>プロパティ ' ' のコード生成に \<property name> 失敗しました

これは、エラーの一般的なラッパーです。 このメッセージに付随するエラー文字列は、エラーメッセージに関する詳細情報を提供し、より具体的なヘルプトピックへのリンクを提供します。 このエラーを修正するには、エラーメッセージに示されたエラーをこのエラーに追加します。

### <a name="component-component-name-did-not-call-containeradd-in-its-constructor"></a>コンポーネント ' \<component name> ' が Container. Add () をコンストラクターで呼び出しませんでした

これは、読み込んだコンポーネントまたはフォームに配置したコンポーネントのエラーです。 これは、コンポーネントがそれ自体をコンテナーコントロールに追加しなかったことを示します (別のコントロールまたはフォームであるかどうか)。 デザイナーは引き続き機能しますが、実行時にコンポーネントに問題がある可能性があります。

このエラーを解決するには、コンポーネントのベンダに問い合わせてください。 または、作成したコンポーネントの場合は、 `IContainer.Add` コンポーネントのコンストラクターでメソッドを呼び出します。

### <a name="component-name-cannot-be-empty"></a>コンポーネント名を空にすることはできません。

このエラーは、コンポーネントの名前を空の値に変更しようとした場合に発生します。

### <a name="could-not-access-the-variable-variable-name-because-it-has-not-been-initialized-yet"></a>変数 ' \<variable name> ' はまだ初期化されていないため、アクセスできませんでした

このエラーは、2つのシナリオが原因で発生する可能性があります。 サードパーティのコンポーネントベンダーが、配布されたコントロールまたはコンポーネントに問題があるか、または記述したコードにコンポーネント間の再帰的な依存関係があります。

このエラーを修正するには、コードに再帰的な依存関係がないことを確認します。 このような問題がない場合は、エラーメッセージのテキストを正確に確認し、コンポーネントのベンダに問い合わせてください。

### <a name="could-not-find-type-type-name"></a>型 ' ' が見つかりませんでした。 \<type name>

エラーメッセージ: "型 ' ' が見つかりませんでした \<type name> 。 この型を含むアセンブリが参照されていることを確認してください。 この型が開発プロジェクトの一部である場合は、プロジェクトが正常にビルドされていることを確認してください。 "

このエラーは、参照が見つからなかったために発生しました。 エラーメッセージに示されている型が参照されていること、および型が必要とするすべてのアセンブリも参照されていることを確認します。 多くの場合、問題は、ソリューション内のコントロールがビルドされていないことです。 ビルドするには、[**ビルド**] メニューの [**ソリューションのビルド**] を選択します。 それ以外の場合、コントロールが既にビルドされている場合は、ソリューションエクスプローラーの [**参照**] または [**依存関係**] フォルダーの右クリックメニューから手動で参照を追加します。

### <a name="could-not-load-type-type-name"></a>型 ' ' を読み込めませんでした \<type name>

エラーメッセージ: "型 ' ' を読み込めませんでした \<type name> 。 この型を含むアセンブリがプロジェクト参照に追加されていることを確認してください。 "

Visual Studio がイベント処理メソッドを接続しようとしましたが、メソッドのパラメーターの型が1つ以上見つかりませんでした。 これは通常、参照がないことが原因で発生します。 このエラーを修正するには、型を含む参照をプロジェクトに追加してから、操作をやり直してください。

### <a name="could-not-locate-the-project-item-templates-for-inherited-components"></a>継承コンポーネントのプロジェクト項目テンプレートが見つかりませんでした。

Visual Studio での継承されたフォームのテンプレートは使用できません。 このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="delegate-class-class-name-has-no-invoke-method-is-this-class-a-delegate"></a>デリゲートクラス ' \<class name> ' に invoke メソッドがありません。 このクラスはデリゲートですか?

Visual Studio でイベントハンドラーを作成しようとしましたが、イベントの種類に問題があります。 これは、イベントが CLS に準拠していない言語で作成された場合に発生する可能性があります。 コンポーネントのベンダにお問い合わせください。

### <a name="duplicate-declaration-of-member-member-name"></a>メンバー ' ' の宣言が重複しています。 \<member name>

このエラーは、メンバー変数が2回宣言されているために発生します (たとえば、という名前の2つのコントロール `Button1` がコード内で宣言されている場合)。 名前は、継承されたフォーム全体で一意である必要があります。 また、大文字と小文字のみを区別して名前を変えることはできません。

### <a name="error-reading-resources-from-the-resource-file-for-the-culture-culture-name"></a>カルチャ ' ' のリソースファイルからリソースを読み取り中にエラーが発生した \<culture name>

このエラーは、プロジェクト内に無効な .resx ファイルがある場合に発生する可能性があります。

このエラーを修正するには、次のようにします。

1. ソリューションエクスプローラーの [**すべてのファイルを表示**] ボタンをクリックして、ソリューションに関連付けられている .resx ファイルを表示します。
2. .Resx ファイルを右クリックし、[**開く**] を選択して、XML エディターで .resx ファイルを読み込みます。
3. .Resx ファイルを手動で編集して、エラーに対処します。

### <a name="error-reading-resources-from-the-resource-file-for-the-default-culture-culture-name"></a>既定のカルチャ ' ' のリソースファイルからリソースを読み取り中にエラーが発生した \<culture name>

このエラーは、既定のカルチャのプロジェクトに無効な .resx ファイルがある場合に発生する可能性があります。

このエラーを修正するには、次のようにします。

1. ソリューションエクスプローラーの [**すべてのファイルを表示**] ボタンをクリックして、ソリューションに関連付けられている .resx ファイルを表示します。
2. .Resx ファイルを右クリックし、[**開く**] を選択して、XML エディターで .resx ファイルを読み込みます。
3. .Resx ファイルを手動で編集して、エラーに対処します。

### <a name="failed-to-parse-method-method-name"></a>メソッド ' ' を解析できませんでした \<method name>

エラーメッセージ: "メソッド ' ' を解析できませんでした \<method name> 。 パーサーから次のエラーが報告されました: ' \<error string> '。 考えられるエラーについては、タスク一覧を参照してください。 "

これは、解析中に発生した問題の一般的なエラーメッセージです。 これらのエラーは、多くの場合、構文エラーによって発生します。 エラーに関連する特定のメッセージについては、タスク一覧を参照してください。

### <a name="invalid-component-name-component-name"></a>無効なコンポーネント名: ' \<component name> '

コンポーネントの名前を、その言語の無効な値に変更しようとしました。 このエラーを修正するには、その言語の名前付け規則に準拠するようにコンポーネントの名前を指定します。

### <a name="the-type-class-name-is-made-of-several-partial-classes-in-the-same-file"></a>型 ' \<class name> ' は、同じファイル内の複数の部分クラスで構成されています。

[Partial](../../../csharp/language-reference/keywords/partial-type.md)キーワードを使用して複数のファイルでクラスを定義する場合、各ファイルに定義できる部分定義は1つだけです。

このエラーを修正するには、クラスの部分定義を1つだけ残して、ファイルからすべて削除します。

### <a name="the-assembly-assembly-name-could-not-be-found"></a>アセンブリ ' \<assembly name> ' が見つかりませんでした。

エラーメッセージ: "アセンブリ ' \<assembly name> ' が見つかりませんでした。 アセンブリが参照されていることを確認します。 アセンブリが現在の開発プロジェクトの一部である場合は、プロジェクトがビルドされていることを確認します。

このエラーは、"型 ' \<type name> ' が見つかりませんでした" と似ていますが、通常、このエラーはメタデータ属性が原因で発生します。 このエラーを修正するには、属性で使用されているすべてのアセンブリが参照されていることを確認します。

### <a name="the-assembly-name-assembly-name-is-invalid"></a>アセンブリ名 ' \<assembly name> ' が無効です。

コンポーネントが特定のアセンブリを要求しましたが、コンポーネントによって指定された名前は有効なアセンブリ名ではありません。 コンポーネントのベンダにお問い合わせください。

### <a name="the-base-class-class-name-cannot-be-designed"></a>基底クラス ' \<class name> ' をデザインできません。

Visual Studio によってクラスが読み込まれましたが、クラスの実装者がデザイナーを提供していないため、クラスをデザインできません。 クラスがデザイナーをサポートしている場合は、コンパイラエラーなど、デザイナーでの表示に問題が発生する問題がないことを確認してください。 また、クラスへのすべての参照が正しいこと、およびすべてのクラス名のスペルが正しいことを確認します。 それ以外の場合、クラスがデザイン可能でない場合は、コードビューで編集します。

### <a name="the-base-class-class-name-could-not-be-loaded"></a>基底クラス ' \<class name> ' を読み込めませんでした

クラスがプロジェクト内で参照されていないため、Visual Studio はこのクラスを読み込むことができません。 このエラーを修正するには、プロジェクトのクラスへの参照を追加し、Windows フォームデザイナーウィンドウを閉じてから再度開きます。

### <a name="the-class-class-name-cannot-be-designed-in-this-version-of-visual-studio"></a>クラス ' \<class name> ' をこのバージョンの Visual Studio でデザインすることはできません。

このコントロールまたはコンポーネントのデザイナーは、Visual Studio と同じ型をサポートしていません。 コンポーネントのベンダにお問い合わせください。

### <a name="the-class-name-is-not-a-valid-identifier-for-this-language"></a>クラス名が、この言語に有効な識別子ではありません。

ユーザーによって作成されているソースコードのクラス名が、使用されている言語に対して無効です。 このエラーを修正するには、言語の要件に準拠するようにクラスの名前を指定します。

### <a name="the-component-cannot-be-added-because-it-contains-a-circular-reference-to-reference-name"></a>' ' への循環参照が含まれているため、コンポーネントを追加できません。 \<reference name>

コントロールまたはコンポーネントをそれ自体に追加することはできません。 もう1つの状況は、Form1 の別のインスタンスを作成するフォーム (例、Form1) の InitializeComponent メソッドにコードがある場合です。

### <a name="the-designer-cannot-be-modified-at-this-time"></a>現在デザイナーを変更することはできません。

このエラーは、エディター内のファイルが読み取り専用としてマークされている場合に発生します。 ファイルが読み取り専用に設定されていないこと、およびアプリケーションが実行されていないことを確認します。

### <a name="the-designer-could-not-be-shown-for-this-file-because-none-of-the-classes-within-it-can-be-designed"></a>このファイルのデザイナーに、デザインできるクラスがないため、デザイナーを表示できませんでした。

このエラーは、Visual Studio がデザイナーの要件を満たす基底クラスを見つけられない場合に発生します。 フォームとコントロールは、デザイナーをサポートする基本クラスから派生する必要があります。 継承されたフォームまたはコントロールから派生している場合は、プロジェクトがビルドされていることを確認します。

### <a name="the-designer-for-base-class-class-name-is-not-installed"></a>基底クラス ' ' のデザイナー \<class name> がインストールされていません。

クラスのデザイナーを読み込むことができませんでした。 このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="the-designer-must-create-an-instance-of-type-type-name-but-it-cant-because-the-type-is-declared-as-abstract"></a>デザイナーは型 ' ' のインスタンスを作成する必要があります \<type name> が、型が abstract として宣言されているため、これを行うことはできません。

このエラーは、デザイナーに渡されるオブジェクトの基底クラスが[abstract](../../../csharp/language-reference/keywords/abstract.md)であり、許可されていないために発生しました。

### <a name="the-file-could-not-be-loaded-in-the-designer"></a>ファイルをデザイナーに読み込めませんでした。

このファイルの基底クラスは、デザイナーをサポートしていません。 この問題を回避するには、コードビューを使用してファイルを操作します。 ソリューションエクスプローラーでファイルを右クリックし、[**コードの表示**] を選択します。

### <a name="the-language-for-this-file-does-not-support-the-necessary-code-parsing-and-generation-services"></a>このファイルの言語は、サービスを解析して生成するのに必要なコードをサポートしません。

エラーメッセージ: "このファイルの言語は、必要なコード解析および生成サービスをサポートしていません。 開いているファイルがプロジェクトのメンバーであることを確認してから、もう一度ファイルを開いてください。

このエラーは、通常、デザイナーをサポートしていないプロジェクト内のファイルを開こうとしたことが原因で発生します。

### <a name="the-language-parser-class-class-name-is-not-implemented-properly"></a>言語パーサークラス ' \<class name> ' が正しく実装されていません

エラーメッセージ: "言語パーサークラス ' \<class name> ' が正しく実装されていません。 更新されたパーサーモジュールについては、ベンダーにお問い合わせください。 "

使用中の言語が、正しい基底クラスから派生していないデザイナークラスを登録しています。 使用している言語のベンダにお問い合わせください。

### <a name="the-name-name-is-already-used-by-another-object"></a>名前 ' \<name> ' は、既に別のオブジェクトによって使用されています。

これは、Visual Studio シリアライザーでの内部エラーです。 このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="the-object-object-name-does-not-implement-the-icomponent-interface"></a>オブジェクト ' \<object name> ' は IComponent インターフェイスを実装していません。

Visual Studio はコンポーネントを作成しようとしましたが、作成されたオブジェクトはインターフェイスを実装していません <xref:System.ComponentModel.IComponent> 。 修正方法については、コンポーネントベンダにお問い合わせください。

### <a name="the-object-object-name-returned-null-for-the-property-property-name-but-this-is-not-allowed"></a>オブジェクト ' \<object name> ' はプロパティ ' ' に対して null を返しました \<property name> が、これは許可されていません。

常にオブジェクトを返す必要がある .NET プロパティがいくつかあります。 たとえば、フォームの**controls**コレクションは、コントロールがない場合でも、常にオブジェクトを返す必要があります。

このエラーを修正するには、エラーで指定されたプロパティが null でないことを確認します。

### <a name="the-serialization-data-object-is-not-of-the-proper-type"></a>シリアル化データ オブジェクトの種類が正しくありません。

シリアライザーによって提供されるデータオブジェクトは、現在使用されているシリアライザーに一致する型のインスタンスではありません。 コンポーネントのベンダにお問い合わせください。

### <a name="the-service-service-name-is-required-but-could-not-be-located"></a>サービス ' \<service name> ' は必須ですが、見つかりませんでした。

エラーメッセージ: "サービス ' \<service name> ' は必須ですが、見つかりませんでした。 Visual Studio のインストールに問題がある可能性があります。 "

Visual Studio で必要なサービスが使用できません。 そのデザイナーをサポートしていないプロジェクトを読み込もうとしている場合は、コードエディターを使用して必要な変更を行います。 それ以外の場合、このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="the-service-instance-must-derive-from-or-implement-interface-name"></a>サービスインスタンスは、' ' から派生するか、' ' を実装しなければなりません。 \<interface name>

このエラーは、コンポーネントまたはコンポーネントデザイナーが、インターフェイスとオブジェクトを必要とする**Addservice**メソッドを呼び出したが、指定されたオブジェクトが指定されたインターフェイスを実装していないことを示します。 コンポーネントのベンダにお問い合わせください。

### <a name="the-text-in-the-code-window-could-not-be-modified"></a>コード ウィンドウのテキストを変更できませんでした。

エラーメッセージ: "コードウィンドウ内のテキストを変更できませんでした。 ファイルが読み取り専用ではなく、十分なディスク領域があることを確認してください。 "

このエラーは、ディスク領域またはメモリの問題が原因で Visual Studio がファイルを編集できない場合、またはファイルが読み取り専用としてマークされている場合に発生します。

### <a name="the-toolbox-enumerator-object-only-supports-retrieving-one-item-at-a-time"></a>Toolbox 列挙子オブジェクトは、一度に 1 項目のみの取得をサポートします。

このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="the-toolbox-item-for-component-name-could-not-be-retrieved-from-the-toolbox"></a>' ' のツールボックス項目を \<component name> ツールボックスから取得できませんでした

エラーメッセージ: "' のツールボックス項目を \<component name> ツールボックスから取得できませんでした。 ツールボックス項目を含むアセンブリが正しくインストールされていることを確認します。 ツールボックス項目で次のエラーが発生しました: \<error string> 。 "

問題のコンポーネントが、Visual Studio にアクセスしたときに例外をスローしました。 コンポーネントのベンダにお問い合わせください。

### <a name="the-toolbox-item-for-toolbox-item-name-could-not-be-retrieved-from-the-toolbox"></a>' ' のツールボックス項目を \<Toolbox item name> ツールボックスから取得できませんでした

エラーメッセージ: "' のツールボックス項目を \<Toolbox item name> ツールボックスから取得できませんでした。 ツールボックスから項目を削除してから、もう一度追加してみてください。 "

このエラーは、ツールボックス項目内のデータが破損した場合、またはコンポーネントのバージョンが変更された場合に発生します。 ツールボックスから項目を削除してから再度追加してみてください。

### <a name="the-type-type-name-could-not-be-found"></a>型 ' \<type name> ' が見つかりませんでした。

エラーメッセージ: "型 ' \<type name> ' が見つかりませんでした。 型を含むアセンブリが参照されていることを確認します。 アセンブリが現在の開発プロジェクトの一部である場合は、プロジェクトがビルドされていることを確認します。

デザイナーの読み込み中に、Visual Studio が型を見つけることができませんでした。 型を含むアセンブリが参照されていることを確認します。 アセンブリが現在の開発プロジェクトの一部である場合は、プロジェクトがビルドされていることを確認します。

### <a name="the-type-resolution-service-may-only-be-called-from-the-main-application-thread"></a>型の解決サービスはメイン アプリケーション スレッドからのみ呼び出されます。

Visual Studio が、間違ったスレッドから必要なリソースにアクセスしようとしました。 このエラーは、デザイナーの作成に使用されたコードが、メインアプリケーションスレッド以外のスレッドからの型解決サービスを呼び出したときに表示されます。 このエラーを修正するには、正しいスレッドからサービスを呼び出すか、コンポーネントベンダに問い合わせてください。

### <a name="the-variable-variable-name-is-either-undeclared-or-was-never-assigned"></a>変数 ' \<variable name> ' は宣言されていないか、割り当てられていません。

ソースコードに、宣言または割り当てられていない**Button1**などの変数への参照が含まれています。 変数が割り当てられていない場合、このメッセージはエラーではなく警告として表示されます。

### <a name="there-is-already-a-command-handler-for-the-menu-command-menu-command-name"></a>メニューコマンド ' ' のコマンドハンドラーが既に存在します。 \<menu command name>

このエラーは、サードパーティのデザイナーが、既にハンドラーを持つコマンドをコマンドテーブルに追加した場合に発生します。 コンポーネントのベンダにお問い合わせください。

### <a name="there-is-already-a-component-named-component-name"></a>' ' という名前のコンポーネントは既に存在します。 \<component name>

エラーメッセージ: "' ' という名前のコンポーネントは既に存在 \<component name> します。 コンポーネントには一意の名前を指定する必要があり、名前の大文字と小文字は区別されません。 名前は、継承されたクラスのコンポーネントの名前と競合することもできません。 "

このエラーメッセージは、プロパティウィンドウ内のコンポーネントの名前が変更された場合に発生します。 このエラーを修正するには、すべてのコンポーネント名が一意であり、大文字と小文字が区別されず、継承されたクラスのコンポーネントの名前と競合しないようにします。

### <a name="there-is-already-a-toolbox-item-creator-registered-for-the-format-format-name"></a>' ' の形式で既にツールボックスアイテム作成者が登録されています。 \<format name>

サードパーティのコンポーネントは、[ツールボックス] タブ上のアイテムへのコールバックを作成しましたが、そのアイテムには既にコールバックが含まれていました。 コンポーネントのベンダにお問い合わせください。

### <a name="this-language-engine-does-not-support-a-codemodel-with-which-to-load-a-designer"></a>この言語エンジンは、デザイナーを読み込む CodeModel をサポートしません。

このメッセージは、"このファイルの言語は、必要なコード解析および生成サービスをサポートしていません" と似ていますが、このメッセージには内部登録の問題が含まれます。 このエラーが表示された場合は、[[問題の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] を使用して問題をログに記録してください。

### <a name="type-type-name-does-not-have-a-constructor-with-parameters-of-types-parameter-type-names"></a>型 ' \<type name\> ' には、型 ' ' のパラメーターを持つコンストラクターがありません。 \<parameter type names>

パラメーターが一致する[コンストラクター](../../../csharp/programming-guide/classes-and-structs/constructors.md)が見つかりませんでした。 これは、必要な型以外の型を持つコンストラクターを指定したことが原因である可能性があります。 たとえば、**ポイント**コンストラクターは2つの整数を受け取ることができます。 Float を指定した場合、このエラーが発生します。

このエラーを修正するには、別のコンストラクターを使用するか、コンストラクターによって提供されるものと一致するようにパラメーター型を明示的にキャストします。

### <a name="unable-to-add-reference-reference-name-to-the-current-application"></a>参照 ' \<reference name> ' を現在のアプリケーションに追加できません

エラーメッセージ: "参照 ' \<reference name> ' を現在のアプリケーションに追加できません。 ' ' の別のバージョンがまだ参照されていないことを確認 \<reference name> してください。

Visual Studio は参照を追加できません。 このエラーを修正するには、参照の別のバージョンがまだ参照されていないことを確認します。

### <a name="unable-to-check-out-the-current-file"></a>現在のファイルをチェックアウトできません。

エラーメッセージ: "現在のファイルをチェックアウトできません。 ファイルがロックされているか、ファイルを手動でチェックアウトする必要がある可能性があります。

このエラーは、現在ソースコード管理にチェックインされているファイルを変更した場合に発生します。 通常、Visual Studio では、ユーザーがファイルをチェックアウトできるように、[ファイルのチェックアウト] ダイアログボックスが表示されます。 今回は、ファイルがチェックアウトされていませんでした。チェックアウト中のマージの競合が原因である可能性があります。 このエラーを修正するには、ファイルがロックされていないことを確認してから、手動でファイルをチェックアウトしてみてください。

### <a name="unable-to-find-page-named-options-dialog-box-tab-name"></a>' ' という名前のページが見つかりません \<Options dialog box tab name>

このエラーは、コンポーネントデザイナーが、存在しない名前を使用して [オプション] ダイアログボックスからページへのアクセスを要求した場合に発生します。 コンポーネントのベンダにお問い合わせください。

### <a name="unable-to-find-property-property-name-on-page-options-dialog-box-tab-name"></a>プロパティ ' \<property name> ' がページ ' ' で見つかりません。 \<Options dialog box tab name>

このエラーは、コンポーネントデザイナーが [オプション] ダイアログボックスからページの特定の値へのアクセスを要求したが、その値が存在しない場合に発生します。 コンポーネントのベンダにお問い合わせください。

### <a name="visual-studio-cannot-open-a-designer-for-the-file-because-the-class-within-it-does-not-inherit-from-a-class-that-can-be-visually-designed"></a>Visual Studio 内のクラスが、画面上でデザインできるクラスから継承されていないため、ファイルのデザイナーを開けません。

Visual Studio はクラスをロードしましたが、そのクラスのデザイナーをロードできませんでした。 Visual Studio では、デザイナーがファイルの最初のクラスを使用する必要があります。 このエラーを修正するには、ファイルの最初のクラスになるようにクラスコードを移動してから、デザイナーを再度読み込みます。

### <a name="visual-studio-cannot-save-or-load-instances-of-the-type-type-name"></a>Visual Studio で、型 ' ' のインスタンスを保存または読み込むことができません \<type name>

これは、サードパーティのコンポーネントに問題があります。 コンポーネントのベンダにお問い合わせください。

### <a name="visual-studio-is-unable-to-open-document-name-in-design-view"></a>Visual Studio はデザインビューで ' ' を開くことができません \<document name>

エラーメッセージ: デザインビューで "Visual Studio は ' ' を開くことができません \<document name> 。 ファイルの種類に対してパーサーがインストールされていません。 "

このエラーは、プロジェクトの言語がデザイナーをサポートしていないことを示します。また、[ファイルを開く] ダイアログボックスまたはソリューションエクスプローラーからファイルを開こうとすると発生します。 代わりに、コードビューでファイルを編集します。

### <a name="visual-studio-was-unable-to-find-a-designer-for-classes-of-type-type-name"></a>' ' 型のクラスのデザイナーが見つかりませんでした \<type name>

Visual Studio によってクラスが読み込まれましたが、クラスをデザインすることはできません。 代わりに、クラスを右クリックして [**コードの表示**] を選択し、コードビューでクラスを編集します。

## <a name="see-also"></a>こちらもご覧ください

- [デザイナーを使用した Windows フォームコントロールの開発](developing-windows-forms-controls-at-design-time.md)
- [Windows フォームデザイナーフォーラム](https://social.msdn.microsoft.com/Forums/windows/home?forum=winformsdesigner)
