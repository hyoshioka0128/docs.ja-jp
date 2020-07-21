---
title: イベントベースの非同期パターンの実装時期を決定する
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: a00046aa-785d-4f7f-a8e5-d06475ea50da
ms.openlocfilehash: c235a838504889a105ef98df47f7373a145503da
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289448"
---
# <a name="deciding-when-to-implement-the-event-based-asynchronous-pattern"></a>イベントベースの非同期パターンの実装時期を決定する

イベント ベースの非同期パターンは、クラスの非同期動作を公開します。 このパターンを導入すると、.NET Framework では、非同期動作を公開する 2 つのパターンが定義されます。<xref:System.IAsyncResult?displayProperty=nameWithType> インターフェイスに基づく非同期パターンとイベント ベースのパターンです。 このトピックでは、両方のパターンをどのような状況で実装するべきか説明します。

<xref:System.IAsyncResult> インターフェイスによる非同期プログラミングについて詳しくは、「[非同期プログラミング モデル (APM)](asynchronous-programming-model-apm.md)」をご覧ください。

## <a name="general-principles"></a>一般原則

一般的に、可能であれば、イベント ベースの非同期パターンを利用して非同期機能を公開してください。 ただし、イベント ベースのパターンでは満たせない要件もあります。 そのようなとき、場合によっては、イベント ベースのパターンに加え、<xref:System.IAsyncResult> パターンも実装する必要があります。

> [!NOTE]
> イベント ベースのパターンを実装せずに <xref:System.IAsyncResult> パターンのみを実装することはまれです。

## <a name="guidelines"></a>ガイドライン

次の一覧は、イベント ベースの非同期パターンを実装するときのガイドラインをまとめたものです。

- 既定の API としてイベント ベースのパターンを使用し、クラスの非同期動作を公開します。

- クラスが主に、Windows フォームなど、クライアント アプリケーションで使用されるとき、<xref:System.IAsyncResult> パターンを公開しないでください。

- 要件を満たすために必要なときにのみ、<xref:System.IAsyncResult> パターンを公開します。 たとえば、既存の API との互換性を得るために <xref:System.IAsyncResult> パターンを公開する必要がある場合です。

- <xref:System.IAsyncResult> パターンを公開するときは、イベント ベースのパターンも公開してください。

- <xref:System.IAsyncResult> パターンを公開する必要がある場合、詳細設定のオプションとしてそれを行います。 たとえば、プロキシ オブジェクトを生成する場合、既定でイベント ベースのパターンを生成し、<xref:System.IAsyncResult> パターンを生成するオプションを指定します。

- <xref:System.IAsyncResult> パターンの実装を基盤にしてイベント ベースのパターンを実装します。

- 同じクラスでイベント ベースのパターンと <xref:System.IAsyncResult> パターンの両方を公開することは避けます。 イベント ベースのパターンを "上位" クラスで公開し、<xref:System.IAsyncResult> パターンを "下位" クラスで公開します。 たとえば、<xref:System.Net.WebClient> コンポーネントのイベント ベースのパターンと <xref:System.Web.HttpRequest> クラスの <xref:System.IAsyncResult> パターンを比較します。

  - 互換性のために必要なとき、イベント ベースのパターンと <xref:System.IAsyncResult> パターンを同じクラスで公開します。 たとえば、<xref:System.IAsyncResult> パターンを使用する API を既に公開している場合、後方互換性のために <xref:System.IAsyncResult> パターンを維持する必要があります。

  - 最終的なオブジェクト モデルが複雑すぎて実装を分ける意味がなくなってしまう場合、イベント ベースのパターンと <xref:System.IAsyncResult> パターンを同じクラスで公開します。 イベント ベースのパターンを公開することを避けるより、1 つのクラスで両方のパターンを公開するほうが得策です。

  - イベント ベースのパターンと <xref:System.IAsyncResult> パターンを 1 つのクラスで公開する必要がある場合、<xref:System.ComponentModel.EditorBrowsableState.Advanced> に設定された <xref:System.ComponentModel.EditorBrowsableAttribute> を使用し、<xref:System.IAsyncResult> パターンの実装を高度な機能として設定します。 これで Visual Studio IntelliSense のようなデザイン環境に、<xref:System.IAsyncResult> のプロパティやメソッドを表示しないように指示されます。 これらのプロパティとメソッドには完全な有用性がまだ与えられていませんが、IntelliSense で開発している開発者は API を詳しく理解できます。

## <a name="criteria-for-exposing-the-iasyncresult-pattern-in-addition-to-the-event-based-pattern"></a>イベント ベースのパターンに加え、IAsyncResult パターンを公開する基準

前述のシナリオではイベント ベースの非同期パターンにさまざまな長所がありましたが、短所もあります。パフォーマンスが最も重要な要件であれば、その短所も考慮してください。

イベント ベースのパターンで <xref:System.IAsyncResult> パターンも対処されないシナリオが 3 つあります。

- 1 つの <xref:System.IAsyncResult> に対する待機をブロックする

- たくさんの <xref:System.IAsyncResult> オブジェクトに対する待機をブロックする

- <xref:System.IAsyncResult> の完了に対するポーリング

以上のシナリオには、イベント ベースのパターンで対処できますが、<xref:System.IAsyncResult> パターンを使用する場合より面倒になります。

開発者は多くの場合、一般的にパフォーマンス要件が非常に高いサービスに <xref:System.IAsyncResult> パターンを使用します。 たとえば、完了のポーリング シナリオに該当するのが高性能サーバーを利用するときです。

また、イベント ベースのパターンは <xref:System.IAsyncResult> パターンと比べて効率性が劣ります。作成されるオブジェクトが多く (特に <xref:System.EventArgs>)、スレッド間で同期がとられるためです。

次の一覧は、<xref:System.IAsyncResult> パターンを使用する場合の推奨事項をいくつか取り上げたものです。

- <xref:System.Threading.WaitHandle> または <xref:System.IAsyncResult> オブジェクトのサポートが厳密に必要な場合にのみ <xref:System.IAsyncResult> パターンを公開します。

- 既存の API で <xref:System.IAsyncResult> パターンを使用している場合にのみ <xref:System.IAsyncResult> パターンを公開します。

- 既存の API が <xref:System.IAsyncResult> パターンに基づく場合、次のリリースでイベント ベースのパターンも公開することを検討します。

- 検証済みの高いパフォーマンス要件がイベント ベースのパターンでは満たせないが、<xref:System.IAsyncResult> パターンでは満たせる場合にのみ、<xref:System.IAsyncResult> パターンを公開します。

## <a name="see-also"></a>参照

- [方法: イベントベースの非同期パターンをサポートするコンポーネントを実装する](component-that-supports-the-event-based-asynchronous-pattern.md)
- [イベント ベースの非同期パターン (EAP)](event-based-asynchronous-pattern-eap.md)
- [イベントベースの非同期パターンの実装](implementing-the-event-based-asynchronous-pattern.md)
- [イベントベースの非同期パターンを実装するための推奨される手順](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [イベントベースの非同期パターンの概要](event-based-asynchronous-pattern-overview.md)
