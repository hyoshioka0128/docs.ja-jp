---
ms.openlocfilehash: ddc98448101c65003001ad05e67f29d75d99ad44
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616090"
---
### <a name="workflowdesignerload-doesnt-remove-symbol-property"></a>WorkflowDesigner.Load ではシンボル プロパティが削除されない

#### <a name="details"></a>説明

ワークフロー デザイナーで .NET Framework 4.5 を対象とし、再ホストされた 3.5 ワークフローを <xref:System.Activities.Presentation.WorkflowDesigner.Load> メソッドで読み込むと、ワークフローの保存中に <xref:System.Xaml.XamlDuplicateMemberException?displayProperty=fullName> がスローされます。

#### <a name="suggestion"></a>提案される解決策

このバグは、ワークフロー デザイナーで .NET Framework 4.5 を対象とするときにのみ現れるため、`WorkflowDesigner.Context.Services.GetService&lt;DesignerConfigurationService&gt;().TargetFrameworkName` を 4.0 の .NET Framework に設定することによって回避できます。あるいは、<xref:System.Activities.Presentation.WorkflowDesigner.Load> の代わりに <xref:System.Activities.Presentation.WorkflowDesigner.Load(System.String)> メソッドを使用してワークフローを読み込むことで問題を回避できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Activities.Presentation.WorkflowDesigner.Load?displayProperty=nameWithType>
