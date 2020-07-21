---
ms.openlocfilehash: ae0c7322b7415157838278b5568e6e49936e9a93
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621243"
---
### <a name="workflow-now-throws-original-exception-instead-of-nullreferenceexception-in-some-cases"></a>場合によって、ワークフローで NullReferenceException ではなく、元の例外がスローされるようになった

#### <a name="details"></a>説明

.NET Framework 4.6.2 ワークフロー アクティビティの Execute メソッドを使用して例外をスローした場合、以前のバージョンで、<code>null</code>値を<xref:System.Exception.Message>プロパティ、System.Activities ワークフロー ランタイムは、スロー、 <xref:System.NullReferenceException?displayProperty=fullName>、マスク、元の例外。 .NET Framework 4.7 以前マスクは、例外がスローされます。

#### <a name="suggestion"></a>提案される解決策

コードが <xref:System.NullReferenceException?displayProperty=fullName> の処理に依存する場合は、カスタム アクティビティからスローされる可能性のある例外をキャッチするように変更します。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.7|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Activities.CodeActivity.Execute(System.Activities.CodeActivityContext)?displayProperty=nameWithType></li><li><xref:System.Activities.AsyncCodeActivity.BeginExecute(System.Activities.AsyncCodeActivityContext,System.AsyncCallback,System.Object)?displayProperty=nameWithType></li><li><xref:System.Activities.AsyncCodeActivity%601.BeginExecute(System.Activities.AsyncCodeActivityContext,System.AsyncCallback,System.Object)?displayProperty=nameWithType></li><li><xref:System.Activities.WorkflowInvoker.Invoke?displayProperty=nameWithType></li></ul>|
