---
title: ASP.NET Web フォームとのアーキテクチャの比較Blazor
description: ASP.NET Web フォームと比較のアーキテクチャについて説明し Blazor ます。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 09/11/2019
ms.openlocfilehash: 51b114c842e131ad9b9a589bf5137a522e135082
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173433"
---
# <a name="architecture-comparison-of-aspnet-web-forms-and-blazor"></a>ASP.NET Web フォームとのアーキテクチャの比較Blazor

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

ASP.NET の Web フォームとには Blazor 多くの類似した概念がありますが、そのしくみには違いがあります。 この章では、ASP.NET Web フォームとの内部の動作とアーキテクチャについて説明し Blazor ます。

## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

ASP.NET Web Forms framework は、ページ中心のアーキテクチャに基づいています。 アプリ内の場所に対する各 HTTP 要求は、ASP.NET が応答する別のページです。 ページが要求されると、ブラウザーのコンテンツは要求されたページの結果に置き換えられます。

ページは次のコンポーネントで構成されています。

- HTML マークアップ
- C# または Visual Basic コード
- ロジックおよびイベント処理機能を含む分離コードクラス
- コントロール

コントロールは、ページ上でプログラムによって配置および操作できる web UI の再利用可能な単位です。 ページは、マークアップ、コントロール、および一部のコードを含む *.aspx*で終わるファイルで構成されます。 分離コードクラスは、使用するプログラミング言語に応じて、同じ基本名と*aspx.cs*または *.aspx*拡張子を持つファイルにあります。 興味深いことに、web サーバーは .aspx ファイルの内容を解釈し、変更されるたびにコンパイルし*ます*。 この再コンパイルは、web サーバーが既に実行されている場合でも発生します。

コントロールは、マークアップを使用して作成し、ユーザーコントロールとして配信できます。 ユーザーコントロールはクラスから派生 `UserControl` し、ページと同様の構造を持ちます。 ユーザーコントロールのマークアップは *.ascx*ファイルに格納されます。 付随する分離コードクラスは、 *ascx.cs*ファイルまたは *.ascx*ファイルに存在します。 コントロールは、またはの基底クラスから継承することにより、コードを使用して完全にビルドすることもでき `WebControl` `CompositeControl` ます。

ページには、広範なイベントライフサイクルもあります。 各ページは、ASP.NET ランタイムが各要求に対してページのコードを実行するときに発生する、初期化、読み込み、prerender、およびアンロードイベントに対してイベントを発生させます。

通常、ページ上のコントロールは、コントロールが表示されるのと同じページにポストバックされ、という名前の非表示フィールドからのペイロードと共に使用され `ViewState` ます。 フィールドには、 `ViewState` コントロールがページに表示されて表示されるときのコントロールの状態に関する情報が含まれています。これにより、ASP.NET ランタイムは、サーバーに送信されたコンテンツの変更を比較および識別できます。

## Blazor

Blazorは、クライアント側の web UI フレームワークであり、角度や反応などの JavaScript フロントエンドフレームワークに似ています。 Blazorユーザー操作を処理し、必要な UI 更新をレンダリングします。 Blazorは、要求/応答モデルに基づいてい*ませ*ん。 ユーザー操作は、特定の HTTP 要求のコンテキストに含まれていないイベントとして処理されます。

Blazorアプリは、HTML ページにレンダリングされる1つ以上のルートコンポーネントで構成されます。

![BlazorHTML のコンポーネント](./media/architecture-comparison/blazor-components-in-html.png)

ユーザーがコンポーネントを表示する場所を指定する方法と、ユーザーの操作のためにコンポーネントを接続する方法は、モデル固有の[ホスト](hosting-models.md)となります。

Blazor[コンポーネント](components.md)は、再利用可能な UI を表す .net クラスです。 各コンポーネントは、独自の状態を保持し、独自のレンダリングロジックを指定します。これには、他のコンポーネントのレンダリングを含めることができます。 コンポーネントは、コンポーネントの状態を更新するために、特定のユーザー操作のイベントハンドラーを指定します。

コンポーネントがイベントを処理した後、は Blazor コンポーネントをレンダリングし、レンダリングされた出力の変更内容を追跡します。 コンポーネントは、ドキュメントオブジェクトモデル (DOM) に直接はレンダリングされません。 代わりに、は、変更を追跡できるように、と呼ばれる DOM のメモリ内表現にレンダリングし `RenderTree` Blazor ます。 Blazor新しくレンダリングされた出力を前の出力と比較して、UI の相違を計算します。これにより、DOM に効率よく適用されます。

![BlazorDOM の相互作用](./media/architecture-comparison/blazor-dom-interaction.png)

また、コンポーネントの状態が通常の UI イベントの外部で変更された場合に、それらのコンポーネントがレンダリングされることを手動で示すこともできます。 Blazor では、`SynchronizationContext` を使用して、1 つの論理スレッドを強制的に実行します。 コンポーネントの ライフサイクル メソッドと Blazor によって発生するイベント コールバックは、この `SynchronizationContext` で実行されます。

>[!div class="step-by-step"]
>[前へ](introduction.md)
>[次へ](hosting-models.md)
