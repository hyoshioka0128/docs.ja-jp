---
ms.openlocfilehash: a007022bf32ffe76861f6f9016a7edace17b0f61
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620355"
---
### <a name="data-written-to-printsystemjobinfojobstream-must-be-in-xps-format"></a>PrintSystemJobInfo.JobStream に書き込まれるデータは XPS 形式とする必要があります

#### <a name="details"></a>説明

<xref:System.Printing.PrintSystemJobInfo.JobStream> プロパティにより印刷ジョブのストリームが公開されます。 ユーザーが基になるオペレーティング システム印刷コンポーネントに生のデータを送信するには、このストリームにデータを書き込みを行います。 .NET Framework 4.5 以降、Windows 8 より後のバージョンの Windows オペレーティング システムでは、このストリームに書き込むデータは XPS 形式のパッケージ ストリームにする必要があります。

#### <a name="suggestion"></a>提案される解決策

印刷内容を出力するには、次のいずれかの操作を行います。<ul><li><xref:System.Windows.Xps.XpsDocumentWriter> クラスを使用して印刷内容を出力します。 これが、推奨される方法です。</li><li><xref:System.Printing.PrintSystemJobInfo.JobStream> プロパティによって返されるストリームに送信されるデータを、XPS 形式のパッケージ ストリームにします。</li></ul>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Printing.PrintSystemJobInfo.JobStream?displayProperty=nameWithType></li></ul>|
